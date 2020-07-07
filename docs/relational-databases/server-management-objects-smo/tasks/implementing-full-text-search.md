---
title: 전체 텍스트 검색 구현
ms.custom: seo-dt-2019
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- full-text search [SMO]
ms.assetid: 9ce9ad9c-f671-4760-90b5-e0c8ca051473
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5660303c542bc77691d0d0f370d8614450a983dc
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008975"
---
# <a name="implementing-full-text-search"></a>전체 텍스트 검색 구현
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  전체 텍스트 검색은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스별로 사용할 수 있으며 SMO에서 <xref:Microsoft.SqlServer.Management.Smo.Server.FullTextService%2A> 개체로 표시됩니다. <xref:Microsoft.SqlServer.Management.Smo.FullTextService> **서버** 개체 아래에 개체를 저장 합니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 전체 텍스트 검색 서비스의 구성 옵션을 관리하는 데 사용됩니다. <xref:Microsoft.SqlServer.Management.Smo.FullTextCatalogCollection> 개체에 속하는 <xref:Microsoft.SqlServer.Management.Smo.Database> 개체는 데이터베이스에 정의된 전체 텍스트 카탈로그를 나타내는 <xref:Microsoft.SqlServer.Management.Smo.FullTextCatalog> 개체 모음입니다. 일반 인덱스와 달리 전체 텍스트 인덱스는 각 테이블에 하나만 정의할 수 있으며 <xref:Microsoft.SqlServer.Management.Smo.FullTextIndexColumn> 개체에서 <xref:Microsoft.SqlServer.Management.Smo.Table> 개체로 표시됩니다.  
  
 전체 텍스트 검색 서비스를 만들려면 데이터베이스에 전체 텍스트 카탈로그를 정의하고 데이터베이스의 테이블 중 하나에 전체 텍스트 검색 인덱스를 정의해야 합니다.  
  
 먼저, <xref:Microsoft.SqlServer.Management.Smo.FullTextCatalog> 생성자를 호출하고 카탈로그 이름을 지정하여 데이터베이스에 전체 텍스트 카탈로그를 만듭니다. 그런 다음 생성자를 호출하고 저장할 테이블을 지정하여 전체 텍스트 인덱스를 만듭니다. 그리고 나서 <xref:Microsoft.SqlServer.Management.Smo.FullTextIndexColumn> 개체를 사용하여 테이블의 열 이름을 지정하면 전체 텍스트 인덱스에 대한 인덱스 열을 추가할 수 있습니다. 그런 다음 생성한 카탈로그에 <xref:Microsoft.SqlServer.Management.Smo.FullTextIndex.CatalogName%2A> 속성을 설정합니다. 마지막으로, <xref:Microsoft.SqlServer.Management.Smo.FullTextIndex.Create%2A> 메서드를 호출하고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 전체 텍스트 인덱스를 만듭니다.  
  
## <a name="example"></a>예제  
 제공된 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual Studio .net에서 Visual C&#35; SMO 프로젝트 만들기](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)를 참조 하세요.  
  
## <a name="creating-a-full-text-search-service-in-visual-basic"></a>Visual Basic에서 전체 텍스트 검색 서비스 만들기  
 이 코드 예제에서는 `ProductCategory` 예제 데이터베이스의 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 테이블에 대한 전체 텍스트 검색 카탈로그를 만듭니다. 그런 다음 `ProductCategory` 테이블의 이름 열에 전체 텍스트 검색 인덱스를 만듭니다. 전체 텍스트 검색 인덱스를 사용하려면 해당 열에 이미 고유 인덱스가 정의되어 있어야 합니다.  
  
```  
' compile with:   
' /r:Microsoft.SqlServer.SqlEnum.dll   
' /r:Microsoft.SqlServer.Smo.dll   
' /r:Microsoft.SqlServer.ConnectionInfo.dll   
' /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Sdk.Sfc  
Imports Microsoft.SqlServer.Management.Common  
  
Public Class A  
   Public Shared Sub Main()  
      ' Connect to the local, default instance of SQL Server.  
      Dim srv As Server = Nothing  
      srv = New Server()  
  
      ' Reference the AdventureWorks database.  
      Dim db As Database = Nothing  
      db = srv.Databases("AdventureWorks")  
  
      ' Reference the ProductCategory table.  
      Dim tb As Table = Nothing  
      tb = db.Tables("ProductCategory", "Production")  
  
      ' Define a FullTextCatalog object variable by specifying the parent database and name arguments in the constructor.  
      Dim ftc As FullTextCatalog = Nothing  
      ftc = New FullTextCatalog(db, "Test_Catalog")  
      ftc.IsDefault = True  
  
      ' Create the Full-Text Search catalog on the instance of SQL Server.  
      ftc.Create()  
  
      ' Define a FullTextIndex object varaible by supplying the parent table argument in the constructor.  
      Dim fti As FullTextIndex = Nothing  
      fti = New FullTextIndex(tb)  
  
      ' Define a FullTextIndexColumn object variable by supplying the parent index and column name arguments in the constructor.  
      Dim ftic As FullTextIndexColumn = Nothing  
      ftic = New FullTextIndexColumn(fti, "Name")  
  
      ' Add the indexed column to the index.  
      fti.IndexedColumns.Add(ftic)  
      fti.ChangeTracking = ChangeTracking.Automatic  
  
      ' Specify the unique index on the table that is required by the Full Text Search index.  
      fti.UniqueIndexName = "AK_ProductCategory_Name"  
  
      ' Specify the catalog associated with the index.  
      fti.CatalogName = "Test_Catalog"  
  
      ' Create the Full Text Search index on the instance of SQL Server.  
      fti.Create()  
   End Sub  
End Class  
```  
  
## <a name="creating-a-full-text-search-service-in-visual-c"></a>Visual C#에서 전체 텍스트 검색 서비스 만들기  
 이 코드 예제에서는 `ProductCategory` 예제 데이터베이스의 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 테이블에 대한 전체 텍스트 검색 카탈로그를 만듭니다. 그런 다음 `ProductCategory` 테이블의 이름 열에 전체 텍스트 검색 인덱스를 만듭니다. 전체 텍스트 검색 인덱스를 사용하려면 해당 열에 이미 고유 인덱스가 정의되어 있어야 합니다.  
  
```  
// compile with:   
// /r:Microsoft.SqlServer.SqlEnum.dll   
// /r:Microsoft.SqlServer.Smo.dll   
// /r:Microsoft.SqlServer.ConnectionInfo.dll   
// /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
using Microsoft.SqlServer.Management.Smo;  
using Microsoft.SqlServer.Management.Sdk.Sfc;  
using Microsoft.SqlServer.Management.Common;  
  
public class A {  
   public static void Main() {  
      // Connect to the local, default instance of SQL Server.  
      Server srv = default(Server);  
      srv = new Server();  
  
      // Reference the AdventureWorks database.  
      Database db = default(Database);  
      db = srv.Databases ["AdventureWorks"];  
  
      // Reference the ProductCategory table.  
      Table tb = default(Table);  
      tb = db.Tables["ProductCategory", "Production"];  
  
      // Define a FullTextCatalog object variable by specifying the parent database and name arguments in the constructor.  
      FullTextCatalog ftc = default(FullTextCatalog);  
      ftc = new FullTextCatalog(db, "Test_Catalog");  
      ftc.IsDefault = true;  
  
      // Create the Full-Text Search catalog on the instance of SQL Server.  
      ftc.Create();  
  
      // Define a FullTextIndex object varaible by supplying the parent table argument in the constructor.  
      FullTextIndex fti = default(FullTextIndex);  
      fti = new FullTextIndex(tb);  
  
      // Define a FullTextIndexColumn object variable by supplying the parent index and column name arguments in the constructor.  
      FullTextIndexColumn ftic = default(FullTextIndexColumn);  
      ftic = new FullTextIndexColumn(fti, "Name");  
  
      // Add the indexed column to the index.  
      fti.IndexedColumns.Add(ftic);  
      fti.ChangeTracking = ChangeTracking.Automatic;  
  
      // Specify the unique index on the table that is required by the Full Text Search index.  
      fti.UniqueIndexName = "AK_ProductCategory_Name";  
  
      // Specify the catalog associated with the index.  
      fti.CatalogName = "Test_Catalog";  
  
      // Create the Full Text Search index on the instance of SQL Server.  
      fti.Create();  
   }  
}  
```  
  
## <a name="creating-a-full-text-search-service-in-powershell"></a>PowerShell에서 전체 텍스트 검색 서비스 만들기  
 이 코드 예제에서는 `ProductCategory` 예제 데이터베이스의 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 테이블에 대한 전체 텍스트 검색 카탈로그를 만듭니다. 그런 다음 `ProductCategory` 테이블의 이름 열에 전체 텍스트 검색 인덱스를 만듭니다. 전체 텍스트 검색 인덱스를 사용하려면 해당 열에 이미 고유 인덱스가 정의되어 있어야 합니다.  
  
```  
# Example of implementing a full text search on the default instance.  
# Set the path context to the local, default instance of SQL Server and database tables  
  
CD \sql\localhost\default\databases  
$db = get-item AdventureWorks2012  
  
CD AdventureWorks\tables  
  
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
  
  
