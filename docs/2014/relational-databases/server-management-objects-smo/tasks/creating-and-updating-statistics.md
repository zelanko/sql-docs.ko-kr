---
title: 작성 및 통계 업데이트 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- statistical information [SMO]
ms.assetid: 47a0a172-a969-4deb-bca9-dd04401a0fe1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 06fee22dc02a543aa9ab8ff249ca26f4cfb4aa40
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63226158"
---
# <a name="creating-and-updating-statistics"></a>통계 생성 및 업데이트
  SMO에서 <xref:Microsoft.SqlServer.Management.Smo.Statistic> 개체를 사용하여 데이터베이스의 쿼리 처리에 대한 통계 정보를 수집할 수 있습니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.Statistic> 및 <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn> 개체를 사용하여 임의 열에 대한 통계를 만드는 것도 가능합니다. <xref:Microsoft.SqlServer.Management.Smo.Statistic.Update%2A> 개체에서 통계를 업데이트하려면 <xref:Microsoft.SqlServer.Management.Smo.Statistic> 메서드를 실행할 수 있습니다. 결과는 쿼리 최적화 프로그램에서 볼 수 있습니다.  
  
## <a name="example"></a>예제  
 제공된 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual Studio.NET에서 Visual Basic SMO 프로젝트 만들기](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) 또는 [Visual C 만들기&#35; Visual Studio.NET에서 SMO 프로젝트](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)합니다.  
  
## <a name="creating-and-update-statistics-in-visual-basic"></a>Visual Basic에서 통계 생성 및 업데이트  
 이 코드 예제는 <xref:Microsoft.SqlServer.Management.Smo.Statistic> 개체 및 <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn> 개체가 만들어지는 기존 데이터베이스에 새 테이블을 만듭니다.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBStatistics1](SMO How to#SMO_VBStatistics1)]  -->  
  
## <a name="creating-and-update-statistics-in-visual-c"></a>Visual C#에서 통계 생성 및 업데이트  
 이 코드 예제는 <xref:Microsoft.SqlServer.Management.Smo.Statistic> 개체 및 <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn> 개체가 만들어지는 기존 데이터베이스에 새 테이블을 만듭니다.  
  
```  
{  
            //Connect to the local, default instance of SQL Server.  
            Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Reference the CreditCard table.   
  
           Table tb = db.Tables["CreditCard", "Sales"];  
            //Define a Statistic object by supplying the parent table and name   
            //arguments in the constructor.   
            Statistic stat = default(Statistic);  
            stat = new Statistic(tb, "Test_Statistics");  
            //Define a StatisticColumn object variable for the CardType column   
            //and add to the Statistic object variable.   
            StatisticColumn statcol = default(StatisticColumn);  
            statcol = new StatisticColumn(stat, "CardType");  
            stat.StatisticColumns.Add(statcol);  
            //Create the statistic counter on the instance of SQL Server.   
            stat.Create();  
        }  
```  
  
## <a name="creating-and-update-statistics-in-powershell"></a>PowerShell에서 통계 생성 및 업데이트  
 이 코드 예제는 <xref:Microsoft.SqlServer.Management.Smo.Statistic> 개체 및 <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn> 개체가 만들어지는 기존 데이터베이스에 새 테이블을 만듭니다.  
  
```  
# Example of implementing a full text search on the default instance.  
# Set the path context to the local, default instance of SQL Server and database tables  
  
CD \sql\localhost\default\databases  
$db = get-item AdventureWorks2012  
  
CD AdventureWorks2012\tables  
  
#Get a reference to the table  
$tb = get-item Production.ProductCategory  
  
# Define a FullTextCatalog object variable by specifying the parent database and name arguments in the constructor.  
  
$ftc = New-Object -TypeName Microsoft.SqlServer.Management.SMO.FullTextCatalog -argumentlist $db, "Test_Catalog2"  
$ftc.IsDefault = $true  
  
# Create the Full Text Search catalog on the instance of SQL Server.  
$ftc.Create()  
  
# Define a FullTextIndex object variable by supplying the parent table argument in the constructor.  
$fti = New-Object -TypeName Microsoft.SqlServer.Management.SMO.FullTextIndex -argumentlist $tb  
  
#  Define a FullTextIndexColumn object variable by supplying the parent index   
#  and column name arguments in the constructor.  
  
$ftic = New-Object -TypeName Microsoft.SqlServer.Management.SMO.FullTextIndexColumn -argumentlist $fti, "Name"  
  
# Add the indexed column to the index.  
$fti.IndexedColumns.Add($ftic)  
  
# Set change tracking  
$fti.ChangeTracking = [Microsoft.SqlServer.Management.SMO.ChangeTracking]::Automatic  
  
# Specify the unique index on the table that is required by the Full Text Search index.  
$fti.UniqueIndexName = "AK_ProductCategory_Name"  
  
# Specify the catalog associated with the index.  
$fti.CatalogName = "Test_Catalog2"  
  
# Create the Full Text Search Index  
$fti.Create()  
```  
  
  
