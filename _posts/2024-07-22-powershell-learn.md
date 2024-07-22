---
layout: post
title: "PowerShell 学习记录"
date: 2024-07-22
tags:
    - windows
    - learn
    - PowerShell
author: "ylvoid"
header-mask: 0.4
header-img: "imgs/page_bg.jpg"
---

# PowerShell基础

PowerShell是windows下的一种命令行工具，一方面它替代了windows原有的cmd命令行，同时新增了名为commond let的新命令，并且它还通过alias的映射，将linux的命令也映射到了commond let中

通过下面的输出可以看出，PowerShell里面有相当多的别名和linux类似，比如ls、cd、cat、cp等，所以不管是从cmd，还是从linux过渡到Windows的PowerShell应该都是挺容易的

以下是通过Get-Alias命令获取到的windows中的映射命令：

```
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           % -> ForEach-Object
Alias           ? -> Where-Object
Alias           ac -> Add-Content
Alias           asnp -> Add-PSSnapin
Alias           cat -> Get-Content
Alias           cd -> Set-Location
Alias           CFS -> ConvertFrom-String                          3.1.0.0    Microsoft.PowerShell.Utility
Alias           chdir -> Set-Location
Alias           clc -> Clear-Content
Alias           clear -> Clear-Host
Alias           clhy -> Clear-History
Alias           cli -> Clear-Item
Alias           clp -> Clear-ItemProperty
Alias           cls -> Clear-Host
Alias           clv -> Clear-Variable
Alias           cnsn -> Connect-PSSession
Alias           compare -> Compare-Object
Alias           copy -> Copy-Item
Alias           cp -> Copy-Item
Alias           cpi -> Copy-Item
Alias           cpp -> Copy-ItemProperty
Alias           curl -> Invoke-WebRequest
Alias           cvpa -> Convert-Path
Alias           dbp -> Disable-PSBreakpoint
Alias           del -> Remove-Item
Alias           diff -> Compare-Object
Alias           dir -> Get-ChildItem
Alias           dnsn -> Disconnect-PSSession
Alias           ebp -> Enable-PSBreakpoint
Alias           echo -> Write-Output
Alias           epal -> Export-Alias
Alias           epcsv -> Export-Csv
Alias           epsn -> Export-PSSession
Alias           erase -> Remove-Item
Alias           etsn -> Enter-PSSession
Alias           exsn -> Exit-PSSession
Alias           fc -> Format-Custom
Alias           fhx -> Format-Hex                                  3.1.0.0    Microsoft.PowerShell.Utility
Alias           fl -> Format-List
Alias           foreach -> ForEach-Object
Alias           ft -> Format-Table
Alias           fw -> Format-Wide
Alias           gal -> Get-Alias
Alias           gbp -> Get-PSBreakpoint
Alias           gc -> Get-Content
Alias           gci -> Get-ChildItem
Alias           gcm -> Get-Command
Alias           gcs -> Get-PSCallStack
Alias           gdr -> Get-PSDrive
Alias           ghy -> Get-History
Alias           gi -> Get-Item
Alias           gjb -> Get-Job
Alias           gl -> Get-Location
Alias           gm -> Get-Member
Alias           gmo -> Get-Module
Alias           gp -> Get-ItemProperty
Alias           gps -> Get-Process
Alias           gpv -> Get-ItemPropertyValue
Alias           group -> Group-Object
Alias           gsn -> Get-PSSession
Alias           gsnp -> Get-PSSnapin
Alias           gsv -> Get-Service
Alias           gu -> Get-Unique
Alias           gv -> Get-Variable
Alias           gwmi -> Get-WmiObject
Alias           h -> Get-History
Alias           history -> Get-History
Alias           icm -> Invoke-Command
Alias           iex -> Invoke-Expression
Alias           ihy -> Invoke-History
Alias           ii -> Invoke-Item
Alias           ipal -> Import-Alias
Alias           ipcsv -> Import-Csv
Alias           ipmo -> Import-Module
Alias           ipsn -> Import-PSSession
Alias           irm -> Invoke-RestMethod
Alias           ise -> powershell_ise.exe
Alias           iwmi -> Invoke-WMIMethod
Alias           iwr -> Invoke-WebRequest
Alias           kill -> Stop-Process
Alias           lp -> Out-Printer
Alias           ls -> Get-ChildItem
Alias           man -> help
Alias           md -> mkdir
Alias           measure -> Measure-Object
Alias           mi -> Move-Item
Alias           mount -> New-PSDrive
Alias           move -> Move-Item
Alias           mp -> Move-ItemProperty
Alias           mv -> Move-Item
Alias           nal -> New-Alias
Alias           ndr -> New-PSDrive
Alias           ni -> New-Item
Alias           nmo -> New-Module
Alias           npssc -> New-PSSessionConfigurationFile
Alias           nsn -> New-PSSession
Alias           nv -> New-Variable
Alias           ogv -> Out-GridView
Alias           oh -> Out-Host
Alias           popd -> Pop-Location
Alias           ps -> Get-Process
Alias           pushd -> Push-Location
Alias           pwd -> Get-Location
Alias           r -> Invoke-History
Alias           rbp -> Remove-PSBreakpoint
Alias           rcjb -> Receive-Job
Alias           rcsn -> Receive-PSSession
Alias           rd -> Remove-Item
Alias           rdr -> Remove-PSDrive
Alias           ren -> Rename-Item
Alias           ri -> Remove-Item
Alias           rjb -> Remove-Job
Alias           rm -> Remove-Item
Alias           rmdir -> Remove-Item
Alias           rmo -> Remove-Module
Alias           rni -> Rename-Item
Alias           rnp -> Rename-ItemProperty
Alias           rp -> Remove-ItemProperty
Alias           rsn -> Remove-PSSession
Alias           rsnp -> Remove-PSSnapin
Alias           rujb -> Resume-Job
Alias           rv -> Remove-Variable
Alias           rvpa -> Resolve-Path
Alias           rwmi -> Remove-WMIObject
Alias           sajb -> Start-Job
Alias           sal -> Set-Alias
Alias           saps -> Start-Process
Alias           sasv -> Start-Service
Alias           sbp -> Set-PSBreakpoint
Alias           sc -> Set-Content
Alias           select -> Select-Object
Alias           set -> Set-Variable
Alias           shcm -> Show-Command
Alias           si -> Set-Item
Alias           sl -> Set-Location
Alias           sleep -> Start-Sleep
Alias           sls -> Select-String
Alias           sort -> Sort-Object
Alias           sp -> Set-ItemProperty
Alias           spjb -> Stop-Job
Alias           spps -> Stop-Process
Alias           spsv -> Stop-Service
Alias           start -> Start-Process
Alias           sujb -> Suspend-Job
Alias           sv -> Set-Variable
Alias           swmi -> Set-WMIInstance
Alias           tee -> Tee-Object
Alias           trcm -> Trace-Command
Alias           type -> Get-Content
Alias           wget -> Invoke-WebRequest
Alias           where -> Where-Object
Alias           wjb -> Wait-Job
Alias           write -> Write-Output
```
# 基础使用

常用的如ls、cp、cd等不必多介绍，主要还是介绍PowerShell与常用shell不同的地方

**与 Linux 不同的地方**：

- PowerShell 是 Windows 下的命令行工具，而 Linux 有其自身的命令行环境。
- PowerShell 中的命令和语法与 Linux 有一定的差异。
- PowerShell 对一些命令进行了别名映射，例如将 Linux 中的一些命令如 ls、cd、cp 等通过 alias 映射到了其自身的 commond let 中。

## **命令文件的格式、语法、使用方法**：

- **格式**：PowerShell 脚本文件通常以 `.ps1` 为扩展名。
- **语法**：具有特定的语法规则，包括命令、参数、变量、表达式等。
- **使用方法**：
    - 可以在 PowerShell 终端中直接运行脚本文件，使用命令 `.\脚本文件名.ps1`。
    - 在脚本中可以定义函数、使用循环、条件判断等控制结构。
    - 可以使用变量来存储数据，并进行数据的处理和操作。
    - 支持管道操作，能够将一个命令的输出作为另一个命令的输入。

在 PowerShell 中，命令文件（脚本）的参数类型主要包括以下几种：

1. **字符串参数（String）**：这是最常见的参数类型，用于表示文本值。例如：`"Hello World"` 。
    - 示例：如果有一个脚本用于打印输入的字符串，可以这样定义参数 `param([string]$message)` ，然后在脚本中使用 `Write-Output $message` 来输出该字符串。
2. **整数参数（Integer）**：用于表示整数值。例如：`10` 、 `5` 。
    - 示例：假设有一个计算阶乘的脚本，参数用于指定要计算阶乘的整数，可以定义参数为 `param([int]$number)` 。
3. **浮点数参数（Float / Double）**：用于表示带有小数部分的数值。例如：`3.14` 、 `1.2e-5` 。
    - 示例：如果有一个计算圆面积的脚本，参数为半径，可以定义为 `param([double]$radius)` 。
4. **布尔参数（Boolean）**：只有两个可能的值：`$true` 和 `$false` 。
    - 示例：比如一个脚本用于决定是否执行某个操作，参数可以定义为 `param([bool]$doAction)` 。
5. **数组参数（Array）**：用于表示一组相同类型的元素。
    - 示例：如果有一个脚本需要处理多个文件名，可以定义参数为 `param([string[]]$fileNames)` 。
6. **哈希表参数（Hash Table）**：也称为字典，是键值对的集合。
    - 示例：假设有一个脚本用于配置一些设置，可以定义参数为 `param([hashtable]$configSettings)` 。
7. **对象参数（Object）**：可以表示各种复杂的对象类型。
    - 示例：如果的脚本需要操作某个特定类型的对象，例如一个自定义的类对象，可以定义参数为 `param([YourCustomObject]$yourObject)` 。

## 示例

以下是一些简单的 PowerShell 命令文件示例：

### **示例 1：打印问候语**

```powershell
param([string]$name)
Write-Output "Hello, $name!"
```

可以这样运行：`.\test.ps1 "John"` ，它将输出 `Hello, John!`

### **示例 2：计算两个数的和**

```powershell
param([int]$num1, [int]$num2)
$sum = $num1 + $num2
Write-Output "The sum of $num1 and $num2 is $sum"
```

运行方式：`.\test.ps1 5 10` ，输出为 `The sum of 5 and 10 is 15`

### **示例 3：列出指定目录下的文件**

```powershell
`param([string]$directory)
Get-ChildItem -Path $directory`
```

比如：`.\test.ps1 "C:\Temp"` ，会列出 `C:\Temp` 目录下的文件和子目录

### **示例 4：判断一个数是否为偶数**

```powershell
param([int]$number)
if ($number % 2 -eq 0) {
    Write-Output "$number is an even number."
} else {
    Write-Output "$number is an odd number."
}
```

运行：`.\test.ps1 12` ，输出 `12 is an even number.`

## 管道

PowerShell 中的管道（Pipeline）允许将一个命令的输出作为另一个命令的输入，从而实现更强大的数据处理和操作。例如，可以使用管道将多个命令组合起来，实现过滤、排序、转换等功能。

例如，以下是一个使用管道的示例：

```powershell
Get-Process | Where-Object {$_.CPU -gt 10} | Sort-Object -Property CPU -Descending
```

在这个示例中，`Get-Process` 命令获取所有进程的信息，然后通过管道将这些信息传递给 `Where-Object` 命令，该命令过滤出 CPU 使用率大于 10 的进程。最后，通过管道将过滤后的进程信息传递给 `Sort-Object` 命令，该命令按照 CPU 使用率降序对进程进行排序。