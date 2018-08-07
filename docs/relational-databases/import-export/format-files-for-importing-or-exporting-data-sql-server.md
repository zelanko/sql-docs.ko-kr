---
title: 데이터를 가져오거나 내보내기 위한 서식 파일(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: import-export
ms.reviewer: ''
ms.suite: sql
ms.technology: data-movement
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- bulk exporting [SQL Server], format files
- bulk importing [SQL Server], format files
- format files [SQL Server]
ms.assetid: b7b97d68-4336-4091-aee4-1941fab568e3
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: bbb109a41bf674399b89943acca173a50a349ed5
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39535383"
---
# <a name="format-files-for-importing-or-exporting-data-sql-server"></a>데이터를 가져오거나 내보내기 위한 서식 파일(SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 데이터를 대량으로 가져오거나 테이블의 데이터를 대량으로 내보내는 경우 *서식 파일* 을 사용하여 데이터를 대량으로 내보내거나 가져오는 데 필요한 모든 서식 정보를 저장할 수 있습니다. 여기에는 해당 테이블을 기준으로 하는 데이터 파일의 각 필드에 대한 서식 정보가 포함됩니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 두 유형의 서식 파일, 즉 XML 서식 및 비 XML 서식 파일을 지원합니다. 비 XML 서식 파일과 XML 서식 파일은 모두 데이터 파일의 각 필드에 대한 설명을 포함하며, XML 서식 파일의 경우에는 해당하는 테이블 열에 대한 설명도 포함합니다. 일반적으로 XML 서식 파일과 비 XML 서식 파일은 서로 전환이 가능하지만 새 서식 파일에는 비 XML 서식 파일에 비해 여러 가지 장점이 있는 XML 구문을 사용하는 것이 좋습니다. 자세한 내용은 [XML 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)의 두 가지 서식 파일 유형을 대량으로 내보내고 가져올 수 있습니다.  
  
  
##  <a name="Benefits"></a> 서식 파일의 이점  
  
-   다른 데이터 형식과 맞추기 위한 편집 작업이 거의 필요 없는 데이터 파일을 작성하거나 다른 소프트웨어의 데이터 파일을 읽는 작업을 유연하게 수행할 수 있습니다.  
  
-   불필요한 데이터를 추가 또는 삭제하거나 데이터 파일에 있는 기존 데이터를 다시 정렬하지 않고도 대량의 데이터를 가져올 수 있습니다. 서식 파일은 데이터 파일의 필드와 테이블의 열이 일치하지 않을 때 특히 유용합니다.  
  
##  <a name="ExamplesOfFFs"></a> 서식 파일의 예  
 다음 예에서는 비 XML 서식 파일 및 XML 서식 파일의 레이아웃을 보여 줍니다. 이러한 서식 파일은 `HumanResources.myTeam` 예제 데이터베이스의 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 테이블에 해당합니다. 이 테이블에는 네 개의 열, 즉 `EmployeeID`, `Name`, `Title` 및 `ModifiedDate`가 있습니다.  
  
> [!NOTE]  
>  이 테이블을 만드는 방법은 [HumanResources.myTeam 예제 테이블&#40;SQL Server&#41;](../../relational-databases/import-export/humanresources-myteam-sample-table-sql-server.md)을 참조하세요.  
  
### <a name="a-using-a-non-xml-format-file"></a>1. 비 XML 서식 파일 사용  
 다음 비 XML 서식 파일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 `HumanResources.myTeam` 네이티브 데이터 형식을 사용합니다. 이 서식 파일은 다음 `bcp` 명령을 사용하여 생성됩니다.  
  
```cmd 
bcp AdventureWorks.HumanResources.myTeam format nul -f myTeam.Fmt -n -T   
The contents of this format file are as follows: 9.0  
4  
1       SQLSMALLINT   0       2       ""   1     EmployeeID               ""  
2       SQLNCHAR      2       100     ""   2     Name                     SQL_Latin1_General_CP1_CI_AS  
3       SQLNCHAR      2       100     ""   3     Title                    SQL_Latin1_General_CP1_CI_AS  
4       SQLNCHAR      2       100     ""   4     Background               SQL_Latin1_General_CP1_CI_AS  
```  
  
 자세한 내용은 [비 XML 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)을 참조하세요.  
  
  
### <a name="b-using-an-xml-format-file"></a>2. XML 서식 파일 사용  
 다음 XML 서식 파일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 `HumanResources.myTeam` 네이티브 데이터 형식을 사용합니다. 이 서식 파일은 다음 `bcp` 명령을 사용하여 생성됩니다.  
  
```cmd
bcp AdventureWorks.HumanResources.myTeam format nul -f myTeam.Xml -x -n -T   
```  
  
 서식 파일은 다음을 포함합니다.  
  
```xml
 <?xml version="1.0"?>  
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="NativePrefix" LENGTH="1"/>  
  <FIELD ID="2" xsi:type="NCharPrefix" PREFIX_LENGTH="2" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="NCharPrefix" PREFIX_LENGTH="2" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="4" xsi:type="NCharPrefix" PREFIX_LENGTH="2" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="EmployeeID" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Name" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="3" NAME="Title" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="Background" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
 자세한 내용은 [XML 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)을 참조하세요.  
  
  
##  <a name="WhenFFrequired"></a> 서식 파일이 필요한 경우  
 INSERT ... SELECT * FROM OPENROWSET(BULK...) 문을 사용하는 경우에는 항상 서식 파일이 필요합니다.  
  
-   **bcp** 또는 BULK INSERT의 경우 단순한 상황에서는 필요에 따라 서식 파일을 사용할 수 있으며 필수적인 경우는 많지 않습니다. 그러나 복잡한 대량 가져오기 상황에서는 서식 파일이 필요한 경우가 종종 있습니다.  
  
 다음과 같은 경우에 서식 파일이 필요합니다.  
  
-   동일한 데이터 파일이 스키마가 다른 여러 테이블의 원본으로 사용되는 경우  
  
-   대상 테이블의 열과 데이터 파일의 필드 개수가 다른 경우. 예를 들면 다음과 같은 경우입니다.  
  
    -   대상 테이블에 기본값이 정의되었거나 NULL이 허용된 열이 최소 하나 이상 포함되어 있는 경우  
  
    -   사용자에게 테이블에 있는 하나 이상의 열에 대한 SELECT/INSERT 권한이 없는 경우  
  
    -   하나의 데이터 파일이 스키마가 다른 둘 이상의 테이블에 사용되는 경우  
  
-   데이터 파일과 테이블의 열 순서가 다른 경우  
  
-   데이터 파일의 열 간에 종결 문자나 접두사 길이가 다른 경우  
  
> [!NOTE]  
>  서식 파일이 없는 경우 **bcp** 명령이 지정한 데이터 형식 스위치(**-n**, **-c**, **-w**또는 **-N**) 또는 BULK INSERT 연산에 지정된 DATAFILETYPE 옵션의 데이터 형식을 데이터 파일의 필드를 해석하는 기본 방법으로 사용합니다.  
  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [서식 파일 만들기&#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)  
  
-   [서식 파일을 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [서식 파일을 사용하여 테이블 열 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [서식 파일을 사용하여 데이터 필드 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
  
## <a name="see-also"></a>참고 항목  
 [비 XML 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)   
 [XML 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)   
 [대량 가져오기 또는 대량 내보내기를 위한 데이터 형식&#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)  
  
  
