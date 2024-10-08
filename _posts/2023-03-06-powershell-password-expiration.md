---
layout: post
title:  "Powershell Script: Password expiration notifications"
author: matt
categories: [ technical, security ]
tag: [ Technical ]
image: assets/post-images/frustrated.png
---

It’s a good idea to have a password expiration policy, but how will users know it’s time to change their password? Maybe it expires when they are on vacation or some other inconvenient time. This script will start emailing the user 14 days before their password expires to give them plenty of time to plan ahead. You can even include a link in the email to a page that reminds them of the process to reduce those pesky helpdesk calls and make it less annoying for your users. Win/Win!

```
#Variables Here
###################################################################################################################
$smtpServer = "192.168.17.36"
[int]$expireInDays = "14"
$from = "Helpdesk <helpdesk@mycompany.com>"
[switch]$logging = $true
#Generates a log file and puts it here:
$logPath = "c:\Scripts\PasswordChangeNotification\Reports"
#Enabling testing will run the script and send it to the email below, not the user.
[switch]$testing = $false
$testRecipient = "me@mycompany.com"
[switch]$status = $false
#$reportto
#$interval

###################################################################################################################
$start = [datetime]::Now
$midnight = $start.Date.AddDays(1)
$timeToMidnight = New-TimeSpan -Start $start -end $midnight.Date
$midnight2 = $start.Date.AddDays(2)
$timeToMidnight2 = New-TimeSpan -Start $start -end $midnight2.Date
# System Settings
$textEncoding = [System.Text.Encoding]::UTF8
$today = $start
# End System Settings

# Get Users From AD who are Enabled, Passwords Expire and are Not Currently Expired
Import-Module ActiveDirectory
$padVal = "20"
Write-Output "Script Loaded"
Write-Output "*** Settings Summary ***"
$smtpServerLabel = "SMTP Server".PadRight($padVal," ")
$expireInDaysLabel = "Expire in Days".PadRight($padVal," ")
$fromLabel = "From".PadRight($padVal," ")
$testLabel = "Testing".PadRight($padVal," ")
$testRecipientLabel = "Test Recipient".PadRight($padVal," ")
$logLabel = "Logging".PadRight($padVal," ")
$logPathLabel = "Log Path".PadRight($padVal," ")
$reportToLabel = "Report Recipient".PadRight($padVal," ")
$interValLabel = "Intervals".PadRight($padval," ")
if($testing)
{
    if(($testRecipient) -eq $null)
    {
        Write-Output "No Test Recipient Specified"
        Exit
    }
}
if($logging)
{
    if(($logPath) -eq $null)
    {
        $logPath = $PSScriptRoot
    }
}
Write-Output "$smtpServerLabel : $smtpServer"
Write-Output "$expireInDaysLabel : $expireInDays"
Write-Output "$fromLabel : $from"
Write-Output "$logLabel : $logging"
Write-Output "$logPathLabel : $logPath"
Write-Output "$testLabel : $testing"
Write-Output "$testRecipientLabel : $testRecipient"
Write-Output "$reportToLabel : $reportto"
Write-Output "$interValLabel : $interval"
Write-Output "*".PadRight(25,"*")
$users = get-aduser -filter {(Enabled -eq $true) -and (PasswordNeverExpires -eq $false)} -properties Name, PasswordNeverExpires, PasswordExpired, PasswordLastSet, EmailAddress | where { $_.passwordexpired -eq $false }
# Count Users
$usersCount = ($users | Measure-Object).Count
Write-Output "Found $usersCount User Objects"
# Collect Domain Password Policy Information
$defaultMaxPasswordAge = (Get-ADDefaultDomainPasswordPolicy -ErrorAction Stop).MaxPasswordAge.Days 
Write-Output "Domain Default Password Age: $defaultMaxPasswordAge"
# Collect Users
$colUsers = @()
# Process Each User for Password Expiry
Write-Output "Process User Objects"
foreach ($user in $users)
{
    $Name = $user.Name
    $emailaddress = $user.emailaddress
    $passwordSetDate = $user.PasswordLastSet
    $samAccountName = $user.SamAccountName
    $pwdLastSet = $user.PasswordLastSet
    # Check for Fine Grained Password
    $maxPasswordAge = $defaultMaxPasswordAge
    $PasswordPol = (Get-AduserResultantPasswordPolicy $user) 
    if (($PasswordPol) -ne $null)
    {
        $maxPasswordAge = ($PasswordPol).MaxPasswordAge.Days
    }
    # Create User Object
    $userObj = New-Object System.Object
    $expireson = $pwdLastSet.AddDays($maxPasswordAge)
    $daysToExpire = New-TimeSpan -Start $today -End $Expireson
    # Round Up or Down
    if(($daysToExpire.Days -eq "0") -and ($daysToExpire.TotalHours -le $timeToMidnight.TotalHours))
    {
        $userObj | Add-Member -Type NoteProperty -Name UserMessage -Value "today."
    }
    if(($daysToExpire.Days -eq "0") -and ($daysToExpire.TotalHours -gt $timeToMidnight.TotalHours) -or ($daysToExpire.Days -eq "1") -and ($daysToExpire.TotalHours -le $timeToMidnight2.TotalHours))
    {
        $userObj | Add-Member -Type NoteProperty -Name UserMessage -Value "tomorrow."
    }
    if(($daysToExpire.Days -ge "1") -and ($daysToExpire.TotalHours -gt $timeToMidnight2.TotalHours))
    {
        $days = $daysToExpire.TotalDays
        $days = [math]::Round($days)
        $userObj | Add-Member -Type NoteProperty -Name UserMessage -Value "in $days days."
    }
    $daysToExpire = [math]::Round($daysToExpire.TotalDays)
    $userObj | Add-Member -Type NoteProperty -Name UserName -Value $samAccountName
    $userObj | Add-Member -Type NoteProperty -Name Name -Value $Name
    $userObj | Add-Member -Type NoteProperty -Name EmailAddress -Value $emailAddress
    $userObj | Add-Member -Type NoteProperty -Name PasswordSet -Value $pwdLastSet
    $userObj | Add-Member -Type NoteProperty -Name DaysToExpire -Value $daysToExpire
    $userObj | Add-Member -Type NoteProperty -Name ExpiresOn -Value $expiresOn
    $colUsers += $userObj
}
$colUsersCount = ($colUsers | Measure-Object).Count
Write-Output "$colusersCount Users processed"
$notifyUsers = $colUsers | where { $_.DaysToExpire -le $expireInDays}
$notifiedUsers = @()
$notifyCount = ($notifyUsers | Measure-Object).Count
Write-Output "$notifyCount Users with expiring passwords within $expireInDays Days"
foreach ($user in $notifyUsers)
{
    # Email Address
    $samAccountName = $user.UserName
    $emailAddress = $user.EmailAddress
    # Set Greeting Message
    $name = $user.Name
    $messageDays = $user.UserMessage
    # Subject Setting
    $subject="Your password will expire $messageDays"
    # Email Body Set Here, Note You can use HTML, including Images.
    $body ="
 <p>Dear $name,</p>
 <p>Your Password will expire <span style='color: #ff0000;'>$messageDays</span><br /><br /> <span style='text-decoration: underline;'><strong>To change your password:</strong></span></p>
 <ul>
 <li>From a Windows laptop while in the office, press CTRL-ALT-Delete and select Change Password</li>
 <li>From a PC not in the office or Mac users click here for detailed instructions</a></li>
 </ul>
 <p>After changing your password, please update the password on your mobile device(s).&nbsp;</p>
 <p>If you have any questions or concerns please open a ticket using the email address below.</p>
 <p>Thank you.</p>

 Helpdesk<br/>
 <a href='helpdesk@mycompany.com'>helpdesk@mycompany.com</a><br/>
 800-555-1212<br/>
    "
       
    # If Testing Is Enabled - Email Administrator
    if($testing)
    {
        $emailaddress = $testRecipient
    } # End Testing

    # If a user has no email address listed
    if(($emailaddress) -eq $null)
    {
        $emailaddress = $testRecipient    
    }# End No Valid Email
    $samLabel = $samAccountName.PadRight($padVal," ")
    try
    {
        if($interval)
        {
            $daysToExpire = [int]$user.DaysToExpire
            if(($interval) -Contains($daysToExpire))
            {
                if($status)
                {
                    Write-Output "Sending Email : $samLabel : $emailAddress"
                }
                Send-Mailmessage -smtpServer $smtpServer -from $from -to $emailaddress -subject $subject -body $body -bodyasHTML -priority High -Encoding $textEncoding -ErrorAction Stop
                $user | Add-Member -MemberType NoteProperty -Name SendMail -Value "OK"
            }
            else
            {
                if($status)
                {
                    Write-Output "Sending Email : $samLabel : $emailAddress : Skipped - Interval"
                }
                $user | Add-Member -MemberType NoteProperty -Name SendMail -Value "Skipped - Interval"
            }
        }
        else
        {
            if($status)
            {
                Write-Output "Sending Email : $samLabel : $emailAddress"
            }
            Send-Mailmessage -smtpServer $smtpServer -from $from -to $emailaddress -subject $subject -body $body -bodyasHTML -priority High -Encoding $textEncoding -ErrorAction Stop
            $user | Add-Member -MemberType NoteProperty -Name SendMail -Value "OK"
        }
        
    }
    catch
    {
        $errorMessage = $_.exception.Message
        if($status)
        {
           $errorMessage
        }
        $user | Add-Member -MemberType NoteProperty -Name SendMail -Value $errorMessage    
    }
    $notifiedUsers += $user
}
if($logging)
{
    # Create Log File
    Write-Output "Creating Log File"
    $day = $today.Day
    $month = $today.Month
    $year = $today.Year
    $date = "$month-$day-$year"
    $logFileName = "$date-PasswordLog.csv"
    if(($logPath.EndsWith("\")))
    {
       $logPath = $logPath -Replace ".$"
    }
    $logFile = $logPath, $logFileName -join "\"
    Write-Output "Log Output: $logfile"
    $notifiedUsers | Export-CSV $logFile
    if ($notifiedUsers.Count -eq 0) {
        Add-Content $logFile -Value "No users have passwords expiring in $expireInDays days or less"
    }
    if($reportTo)
    {
        $reportSubject = "Password Expiry Report"
        $reportBody = "Password Expiry Report Attached"
        try {
            Send-Mailmessage -smtpServer $smtpServer -from $from -to $reportTo -subject $reportSubject -body $reportbody -bodyasHTML -priority High -Encoding $textEncoding -Attachments $logFile -ErrorAction Stop 
        }
        catch
        {
            $error = $_.Exception.Message
            Write-Output $error
        }
    }
}
$notifiedUsers | select UserName,Name,EmailAddress,PasswordSet,DaysToExpire,ExpiresOn | sort DaystoExpire | FT -autoSize

$stop = [datetime]::Now
$runTime = New-TimeSpan $start $stop
Write-Output "Script Runtime: $runtime"
# Enddirectory
```