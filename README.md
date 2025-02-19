This project is a fork from https://github.com/MySqlBackupNET/MySqlBackup.Net and should not be long lived.
The main target is to experiment a version supporting the MysqlConnector instead of Mysql.Data legacy provider.

# MySqlBackup.Net

A tool to backup and restore MySQL database in C#/VB.NET/ASP.NET.

Article at [CodeProject.com](http://www.codeproject.com/Articles/256466/MySqlBackup-NET)

## NuGet

https://www.nuget.org/packages/MySqlBackup.NET.MysqlConnector/2.3.4.2

## Donation to This Project

[Stripe Donate](https://buy.stripe.com/dR6aIgawrbUW57GeUU)

## How to Add This Library into Your Project
Read [this wiki: How to Add This Library into Your Project](https://github.com/MySqlBackupNET/MySqlBackup.Net/wiki/How-to-Add-This-Library-into-Your-Project)

## Backup ALL Databases in 1 Click
Export all the databases one by one to separate SQL dump files. This a sub-project expansion using MySqlBackup.NET. Read more: [MySqlBackup_All_DB](https://github.com/MySqlBackupNET/MySqlBackup_All_DB)

## Download
https://github.com/MySqlBackupNET/MySqlBackup.Net/releases

Install via NuGet: **PM> Install-Package MySqlBackup.NET**  
[https://www.nuget.org/packages/MySqlBackup.NET/](https://www.nuget.org/packages/MySqlBackup.NET/)

## Acknowledgement

MySqlBackup.NET stands on top of 2 options of connector:

Option 1: **MySql.Data.DLL**
Developped by MySQL (Oracle), [https://dev.mysql.com/downloads/connector/net/](https://dev.mysql.com/downloads/connector/net/).

Option 2: **Devart dotConnect Express**
Developped by Devart, [https://www.devart.com/dotconnect/mysql/](https://www.devart.com/dotconnect/mysql/).

## Backup/Export a MySQL Database
```C#
string constring = "server=localhost;user=root;pwd=qwerty;database=test;";

// Important Additional Connection Options
constring += "charset=utf8;convertzerodatetime=true;";

string file = "C:\\backup.sql";

using (MySqlConnection conn = new MySqlConnection(constring))
{
    using (MySqlCommand cmd = new MySqlCommand())
    {
        using (MySqlBackup mb = new MySqlBackup(cmd))
        {
            cmd.Connection = conn;
            conn.Open();
            mb.ExportToFile(file);
            conn.Close();
        }
    }
}
```

## Import/Restore a MySQL Database

```C#
string constring = "server=localhost;user=root;pwd=qwerty;database=test;";

// Important Additional Connection Options
constring += "charset=utf8;convertzerodatetime=true;";

string file = "C:\\backup.sql";

using (MySqlConnection conn = new MySqlConnection(constring))
{
    using (MySqlCommand cmd = new MySqlCommand())
    {
        using (MySqlBackup mb = new MySqlBackup(cmd))
        {
            cmd.Connection = conn;
            conn.Open();
            mb.ImportFromFile(file);
            conn.Close();
        }
    }
}
```

## Introduction

MySqlBackup.NET is a tool (DLL) that can backup/restore MySQL database in .NET Programming Language. It is an alternative to MySqlDump.

This tool is developed in C# but able to be used in any .NET Language (i.e. VB.NET, F#, etc.).

Another benefit of making this tool is, we don't have to rely on two small programs - MySqlDump.exe and MySql.exe to perform the backup and restore task. We will have better control on the output result in .NET way.

The most common way to backup a MySQL Database is by using MySqlDump and MySQL Workbench.

MySQL Workbench is good for developers, but when comes to the client or end-user, the recommended way is to get every parameter preset and all they need to know is press the big button "Backup" and everything is done. Using MySQL Workbench as a backup tool is not a suitable solution for the client or end-user.

On the other hand, MySqlDump.exe cannot be executed directly from the Web Server. As most providers forbid that, MySqlBackup will be helpful in building a web-based (ASP.NET) backup tool.

## Features

* Backup and Restore of MySQL Database
* Can be used in any .NET Languages.
* Export/Import to/from MemoryStream
* Conditional Rows Export (Filter Tables or Rows)
* Progress Report is Available for Both Export and Import Task.
* Able to export rows into different modes. (Insert, Insert Ignore, Replace, On Duplicate Key Update, Update)
* Can be used directly in ASP.NET or web services.

## Prerequisite and Dependencies for Development, Compile and Production Usage

MySqlBackup.NET relies on the following component to work.

Option 1: MySql.Data (Connector/NET)
* [MySQL dot net Connector/Net (MySql.Data.DLL)](http://www.mysql.com/downloads/connector/net/)<br />_A reference of this DLL must be added into your project in order for to compile or work with MySqlBackup.NET.<br />MySql.Data.DLL is developed by Oracle Corporation, licensed under GPL License (http://www.gnu.org/licenses/old-licenses/gpl-2.0.html)._
* MySql.Data.DLL

Option 2: Devart Express (dotConnect)
* [Devart dotConnect for MySQL Express](https://www.devart.com/dotconnect/mysql/)<br />_A reference of this DLL must be added into your project in order for to compile or work with MySqlBackup.NET._
* For license agreement, please read: [https://www.devart.com/dotconnect/mysql/licensing-faq.html](https://www.devart.com/dotconnect/mysql/licensing-faq.html)
* Devart.Data.DLL
* Devart.Data.MySql.DLL
## Reminder

### Reminder 1

MySqlBackup.NET (or MySqlBackup.DLL) stands on top of MySql.Data.DLL which also stands on top of .NET Framework, which uses UTF8 encoding by default.
If your database involves any UTF8 or Unicode Characters. You must use a MySQL database with default character of **UTF8** while handling Unicode Characters, such as

* Western European specific languages, the character of 'À', 'ë', 'õ', 'Ñ'.
* Russian, Hebrew, India, Arabic, Chinese, Korean, Japanese characters, etc.

You are recommended to apply the connection string option of charset=utf8. Example:

```
server=localhost;user=root;pwd=mypwd;charset=utf8;
```

### Reminder 2

(For MySql.Data connector only)
DateTime conversion between MySQL and .NET Framework. In MySQL, there are various of DateTime format, such as null value or Date only data. But, in .NET Framework, there is no null value (or Date only) for DateTime. This error is not caused by MySqlBackup.DLL. MySql.Data.DLL (developed by Oracle) has decided to throw an exception of Data Conversion Error. Therefore, you are strongly recommended to apply the connection string option of **convertzerodatetime=true**. Example:

```
server=localhost;user=root;pwd=mypwd;charset=utf8;convertzerodatetime=true;
```



## License

MySqlBackup.Net is licensed under the [The Unlicense](https://github.com/MySqlBackupNET/MySqlBackup.Net/blob/master/LICENSE).
