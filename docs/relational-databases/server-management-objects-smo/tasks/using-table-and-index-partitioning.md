---
title: "테이블 및 인덱스 분할을 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- partitions [SMO]
- storing data [SMO]
- partitioned tables [SQL Server], SMO
- partitioned indexes [SQL Server], SMO
ms.assetid: 0e682d7e-86c3-4d73-950d-aa692d46cb62
caps.latest.revision: "46"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ae5b30ad5cab9d7e9ceb34103e64b7a782367b1e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="using-table-and-index-partitioning"></a>테이블 및 인덱스 분할 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]제공한 저장 알고리즘을 사용 하 여 데이터를 저장할 수 있습니다 [Partitioned Tables and Indexes](../../../relational-databases/partitions/partitioned-tables-and-indexes.md)합니다. 큰 테이블과 인덱스를 분할하면 더 효율적으로 관리 및 확장할 수 있습니다.  
  
## <a name="index-and-table-partitioning"></a>인덱스 및 테이블 분할  
 이 기능을 사용하여 인덱스 및 테이블 데이터를 파티션의 여러 파일 그룹에 분산할 수 있습니다. 파티션 함수는 분할 열이라고 하는 특정 열의 값을 기반으로 파티션 집합에 테이블이나 인덱스의 행을 매핑하는 방식을 정의합니다. 파티션 구성표는 파티션 함수로 지정된 각 파티션을 파일 그룹에 매핑합니다. 이렇게 하면 테이블을 파일 그룹과 물리적 장치로 확장하는 보관 전략을 개발할 수 있습니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.Database> 개체의 컬렉션을 포함 <xref:Microsoft.SqlServer.Management.Smo.PartitionFunction> 구현 된 파티션 함수 및 컬렉션을 나타내는 개체를 <xref:Microsoft.SqlServer.Management.Smo.PartitionScheme> 데이터 파일 그룹에 매핑하는 방법을 설명 하는 개체입니다.  
  
 각 <xref:Microsoft.SqlServer.Management.Smo.Table> 및 <xref:Microsoft.SqlServer.Management.Smo.Index> 개체는 <xref:Microsoft.SqlServer.Management.Smo.PartitionScheme> 속성에 사용할 파티션 구성표를 지정하고 <xref:Microsoft.SqlServer.Management.Smo.PartitionSchemeParameterCollection>에 열을 지정합니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제를 사용하려면 응용 프로그램을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 참조 [만들기 Visual C &#35; Visual Studio.NET에서에서 SMO 프로젝트](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)합니다.  
  
## <a name="setting-up-a-partition-scheme-for-a-table-in-visual-c"></a>Visual C#에서 테이블에 대한 파티션 구성표 설정  
 코드 예제에서는 파티션 함수와 파티션 구성표를 만드는 방법을 보여 줍니다는 `TransactionHistory` 테이블에 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 예제 데이터베이스. 오래된 레코드를 `TransactionHistoryArchive` 테이블에 구분해 두기 위해 파티션은 날짜별로 나뉩니다.  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Reference the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
//Define and create three new file groups on the database.   
FileGroup fg2;   
fg2 = new FileGroup(db, "Second");   
fg2.Create();   
FileGroup fg3;   
fg3 = new FileGroup(db, "Third");   
fg3.Create();   
FileGroup fg4;   
fg4 = new FileGroup(db, "Fourth");   
fg4.Create();   
//Define a partition function by supplying the parent database and name arguments in the constructor.   
PartitionFunction pf;   
pf = new PartitionFunction(db, "TransHistPF");   
//Add a partition function parameter that specifies the function uses a DateTime range type.   
PartitionFunctionParameter pfp;   
pfp = new PartitionFunctionParameter(pf, DataType.DateTime);   
pf.PartitionFunctionParameters.Add(pfp);   
//Specify the three dates that divide the data into four partitions.   
object[] val;   
val = new object[] {"1/1/2003", "1/1/2004", "1/1/2005"};   
pf.RangeValues = val;   
//Create the partition function.   
pf.Create();   
//Define a partition scheme by supplying the parent database and name arguments in the constructor.   
PartitionScheme ps;   
ps = new PartitionScheme(db, "TransHistPS");   
//Specify the partition function and the filegroups required by the partition scheme.   
ps.PartitionFunction = "TransHistPF";   
ps.FileGroups.Add("PRIMARY");   
ps.FileGroups.Add("second");   
ps.FileGroups.Add("Third");   
ps.FileGroups.Add("Fourth");   
//Create the partition scheme.   
ps.Create();   
}   
```  
  
## <a name="setting-up-a-partition-scheme-for-a-table-in-powershell"></a>PowerShell에서 테이블에 대한 파티션 구성표 설정  
 코드 예제에서는 파티션 함수와 파티션 구성표를 만드는 방법을 보여 줍니다는 `TransactionHistory` 테이블에 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 예제 데이터베이스. 오래된 레코드를 `TransactionHistoryArchive` 테이블에 구분해 두기 위해 파티션은 날짜별로 나뉩니다.  
  
```powershell  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default  
  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
$db = $srv.Databases["AdventureWorks"]  
#Create four filegroups  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "First"  
$fg2 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Second"  
$fg3 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Third"  
$fg4 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Fourth"  
  
#Define a partition function by supplying the parent database and name arguments in the constructor.  
$pf =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.PartitionFunction -argumentlist $db, "TransHistPF"  
$T = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$T  
$T.GetType()  
#Add a partition function parameter that specifies the function uses a DateTime range type.  
$pfp =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.PartitionFunctionParameter -argumentlist $pf, $T  
  
#Specify the three dates that divide the data into four partitions.   
#Create an array of type object to hold the partition data  
$val = "1/1/2003"."1/1/2004","1/1/2005"  
$pf.RangeValues = $val  
$pf  
#Create the partition function  
$pf.Create()  
  
#Create partition scheme  
$ps = New-Object -TypeName Microsoft.SqlServer.Management.SMO.PartitionScheme -argumentlist $db, "TransHistPS"  
$ps.PartitionFunction = "TransHistPF"  
  
#add the filegroups to the scheme   
$ps.FileGroups.Add("PRIMARY")  
$ps.FileGroups.Add("Second")  
$ps.FileGroups.Add("Third")  
$ps.FileGroups.Add("Fourth")  
  
#Create it at the server  
$ps.Create()  
```  
  
## <a name="see-also"></a>참고 항목  
 [Partitioned Tables and Indexes](../../../relational-databases/partitions/partitioned-tables-and-indexes.md)  
  
  
