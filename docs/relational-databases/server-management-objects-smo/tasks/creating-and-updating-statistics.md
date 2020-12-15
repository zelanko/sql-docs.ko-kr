---
description: 통계 만들기 및 업데이트
title: 통계 만들기 및 업데이트
ms.prod: sql
ms.prod_service: database-engine
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- statistical information [SMO]
ms.assetid: 47a0a172-a969-4deb-bca9-dd04401a0fe1
author: markingmyname
ms.author: maghan
ms.reviewer: matteot
ms.custom: seo-dt-2019
ms.date: 06/04/2020
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 64b631219afcd37bbc6883ef7e1c89d6335b7095
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475534"
---
# <a name="create-and-update-statistics"></a>통계 만들기 및 업데이트

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

SMO에서 <xref:Microsoft.SqlServer.Management.Smo.Statistic> 개체를 사용하여 데이터베이스의 쿼리 처리에 대한 통계 정보를 수집할 수 있습니다.

및 개체를 사용 하 여 모든 열에 대 한 통계를 만들 수 <xref:Microsoft.SqlServer.Management.Smo.Statistic> <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn> 있습니다. <xref:Microsoft.SqlServer.Management.Smo.Statistic.Update%2A> 개체에서 통계를 업데이트하려면 <xref:Microsoft.SqlServer.Management.Smo.Statistic> 메서드를 실행할 수 있습니다. 결과는 쿼리 최적화 프로그램에서 볼 수 있습니다.

## <a name="example"></a>예

제공 된 코드 예제를 사용 하려면 응용 프로그램을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택할 수 있습니다. 자세한 내용은 [Visual Studio .net에서 Visual C&#35; SMO 프로젝트 만들기](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)를 참조 하세요.

## <a name="create-and-update-statistics-in-visual-basic"></a>Visual Basic에서 통계 만들기 및 업데이트

이 코드 예제는 <xref:Microsoft.SqlServer.Management.Smo.Statistic> 개체 및 <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn> 개체가 만들어지는 기존 데이터베이스에 새 테이블을 만듭니다.

```vb
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Reference the CreditCard table.
Dim tb As Table
tb = db.Tables("CreditCard", "Sales")
'Define a Statistic object by supplying the parent table and name arguments in the constructor.
Dim stat As Statistic
stat = New Statistic(tb, "Test_Statistics")
'Define a StatisticColumn object variable for the CardType column and add to the Statistic object variable.
Dim statcol As StatisticColumn
statcol = New StatisticColumn(stat, "CardType")
stat.StatisticColumns.Add(statcol)
'Create the statistic counter on the instance of SQL Server.
stat.Create()
```

## <a name="create-and-update-statistics-in-c"></a>C에서 통계 생성 및 업데이트 #

이 코드 예제는 <xref:Microsoft.SqlServer.Management.Smo.Statistic> 개체 및 <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn> 개체가 만들어지는 기존 데이터베이스에 새 테이블을 만듭니다.

```csharp
public static void CreatingAndUpdatingStatistics()
{
    // Connect to the local, default instance of SQL Server.
    var srv = new Server();

    // Reference the AdventureWorks2012 database.
    var db = srv.Databases["AdventureWorks"];

    // Reference the CreditCard table.
    var tb = db.Tables["CreditCard", "Sales"];

    // Define a Statistic object by supplying the parent table and name
    // arguments in the constructor.
    var stat = new Statistic(tb, "Test_Statistics");

    // Define a StatisticColumn object variable for the CardType column
    // and add to the Statistic object variable.
    var statcol = new StatisticColumn(stat, "CardType");
    stat.StatisticColumns.Add(statcol);

    //Create the statistic counter on the instance of SQL Server.
    stat.Create();

    // List all the statistics object on the table (you will see the newly created one)
    foreach (var s in tb.Statistics.Cast<Statistic>())
        Console.WriteLine($"{s.ID}\t{s.Name}");

    // Output:
    //  2       AK_CreditCard_CardNumber
    //  1       PK_CreditCard_CreditCardID
    //  3       Test_Statistics
 }
```

## <a name="create-and-update-statistics-in-powershell"></a>PowerShell에서 통계 생성 및 업데이트

이 코드 예제는 <xref:Microsoft.SqlServer.Management.Smo.Statistic> 개체 및 <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn> 개체가 만들어지는 기존 데이터베이스에 새 테이블을 만듭니다.

```powershell
Import-Module SQLServer

# Connect to the local, default instance of SQL Server.  
$srv = Get-Item SQLSERVER:\SQL\localhost\DEFAULT

# Reference the AdventureWorks database.
$db = $srv.Databases["AdventureWorks"]

# Reference the CreditCard table.
$tb = $db.Tables["CreditCard", "Sales"]

# Define a Statistic object by supplying the parent table and name
# arguments in the constructor.
$stat = New-Object Microsoft.SqlServer.Management.Smo.Statistic($tb, "Test_Statistics")

# Define a StatisticColumn object variable for the CardType column
# and add to the Statistic object variable.
$statcol = New-Object Microsoft.SqlServer.Management.Smo.StatisticColumn($stat, "CardType")
$stat.StatisticColumns.Add($statcol)

# Create the statistic counter on the instance of SQL Server.
$stat.Create()

# Finally dump all the statistics (you can see the newly created one at the bottom)
$tb.Statistics

# Output:
# Name                                Last Updated Is From Index  Statistic Columns
#                                                  Creation
# ----                                ------------ -------------- -----------------
# AK_CreditCard_CardNumber      10/27/2017 2:33 PM True           {CardNumber}
# PK_CreditCard_CreditCardID    10/27/2017 2:33 PM True           {CreditCardID}
# Test_Statistics                 6/4/2020 8:11 PM False          {CardType}
```
