---
layout: post
title:  "Powershell Script: Vulnerability Scan Report — Check the KEV"
author: matt
categories: [ technical, security ]
tag: [ Technical ]
image: assets/post-images/address-10k-vulns.jpg
---


As part of a vulnerability management program its important to run a vulnerability scan of your systems on a regular basis. When the scan is complete there are usually thousands of vulnerabilities identified. Customers frequently ask how they should prioritize remediating those vulnerabilities since nobody has time to do them all.

A common answer is to just worry about the Critical vulnerabilies. The problem with this approach is that the vast majority of vulnerabilies that are actually exploited are not rated as Critical. Many of them are High, Medium or even Low. Only addressing the Critical vulnerabilities is going to leave you with a lot of exposure.

Wouldn’t it be nice if you could prioritize those vulnerabilities based on which ones are known to be actively exploited? Well, you can. There are sophisticated (and expensive) tools which will help you do this but here is a free and easy way to do it yourself.

[CISA](https://www.cisa.gov), the Cybersecurity and Infrastructure Security Agency maintains a list known exploited vulnerabilities (KEV). You can download it directly from the website [here](https://www.cisa.gov/known-exploited-vulnerabilities-catalog) but then you have to sift through that file and compare it with your vulnerability scan. How tedious.

Here I have created a Powershell script which will download the latest version of the KEV to your computer, ask you for a CSV version of your vulnerability scan report and compare the two. Matches will be outputted to a file. You may need to customize the script depending on the column names in your CSV file. This script was written to work with [Nessus](https://www.tenable.com/products/nessus), a very common vulnerability scanner maintaned by Tenable.

```
#This script will take a CSV output from a vulnerability scan and compare it with the CISA Known Exploited Vulnerabilties list and output a report on any matches.

#First, lets download the current KEV from CISA. The file will drop in whatever directory this script is running in.

Invoke-WebRequest -Uri "https://www.cisa.gov/sites/default/files/csv/known_exploited_vulnerabilities.csv" -OutFile ".\known_exploited_vulnerabilities.csv"

#Then, lets ask the user for the CSV to be evaluated. This will open a dialog box for the user to locate the file.

Add-Type -AssemblyName System.Windows.Forms
$FileBrowser = New-Object System.Windows.Forms.OpenFileDialog -Property @{
    InitialDirectory = [Environment]::GetFolderPath('Desktop') 
    Filter = 'CSV (*.csv) |*.csv'
    }
$null = $FileBrowser.ShowDialog()

#CSV1 is the file we downloaded from CISA (KEV)
#CSV2 is the file we selected above in the from the FileBrowser

$csv1 = Import-Csv -Path ".\known_exploited_vulnerabilities.csv"
$csv2 = Import-Csv $FileBrowser.FileName
$combine = @()

#Loop through the files to compare.

foreach ($first in $csv1) {
  foreach ($second in $csv2) {
    if ($second.'CVE' -eq $first.'cveID') {

#You will need to update each of these to match the column headers in your CSV file and output the columns you want in the output file. 
#Be sure that the values in the CVE column of your file are in the format of 'CVE-DDDD-XXXX' or it will not match the KEV giving invalid results. 
        $match = New-Object PSObject
        $match | Add-Member Noteproperty "CVE" $second.'CVE'
        $match | Add-Member Noteproperty "Host" $second.'Host'
        $match | Add-Member Noteproperty "Port" $second.'Port'
        $match | Add-Member Noteproperty "Name" $second.'Name'
        $match | Add-Member Noteproperty "Synopsis" $second.'Synopsis'
        $combine += $match
    }
  }
}
#Output the matches to KEV_Matches.csv otherwise output to the screen and don't generate a file.
if ($combine.length -ne 0) {$combine | Export-Csv -Path ".\KEV_Matches.csv"} else {write-host "No CVE Matches Found. Lucky you! Exiting"}
```