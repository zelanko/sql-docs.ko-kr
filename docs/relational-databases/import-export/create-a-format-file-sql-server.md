---
title: 서식 파일 만들기(SQL Server) | Microsoft 문서
description: SQL Server 테이블을 대량으로 가져오거나 내보낼 때 서식 파일을 사용하면 다른 프로그램의 데이터 파일을 거의 편집하거나 읽지 않고 데이터 파일을 쓸 수 있습니다.
ms.custom: ''
ms.date: 02/23/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- format files [SQL Server], creating
ms.assetid: f680b4a0-630f-4052-9c79-d348c1076f7b
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4b3cffe95dcdd41cc904aed95de0d91c97314670
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009926"
---
# <a name="create-a-format-file-sql-server"></a>서식 파일 만들기
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블로 대량 가져오기를 수행하거나 테이블에서 데이터를 대량 내보내기를 수행할 때는 서식 파일을 사용하여 다른 데이터 형식과 맞추기 위한 편집 작업이 거의 필요 없는 데이터 파일을 작성하거나 다른 소프트웨어 프로그램에서 데이터 파일을 읽는 작업을 유연하게 수행할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 은(는) 두 유형의 서식 파일, 즉 비 XML 서식 파일과 XML 서식 파일을 지원합니다. 비 XML 서식 파일은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 원래 지원했던 서식 파일입니다.  
  
 일반적으로 XML 서식 파일과 비 XML 서식 파일은 서로 전환이 가능하지만 새 서식 파일에는 비 XML 서식 파일에 비해 여러 가지 장점이 있는 XML 구문을 사용하는 것이 좋습니다.  
  
> [!NOTE]  
>  서식 파일을 읽는 데 사용되는 **bcp** 유틸리티(Bcp.exe)의 버전은 서식 파일을 만드는 데 사용되는 버전 이상이어야 합니다. 예를 들어 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] **bcp**는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] **bcp**에서 생성된 버전 10.0 서식 파일을 읽을 수 있지만 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] **bcp**는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] **bcp**에서 생성된 버전 11.0 서식 파일을 읽을 수 없습니다.  
  
 이 항목에서는 [bcp 유틸리티](../../tools/bcp-utility.md) 를 사용하여 특정 테이블에 대한 서식 파일을 만드는 방법에 대해 설명합니다. 서식 파일은 지정된 데이터 형식 옵션( **-n**, **-c**, **-w**또는 **-N**)과 테이블 또는 뷰 구분 기호를 기반으로 합니다.  
  
## <a name="creating-a-non-xml-format-file"></a>비 XML 서식 파일 만들기  
 **bcp** 명령을 사용하여 서식 파일을 만들려면 데이터 파일 경로 대신 **format** 인수를 지정하고 **NUL** 을 사용합니다. **format** 옵션에는 다음과 같이 **-f** 옵션도 필요합니다.  
  
 **bcp** _table_or_view_ **format** nul **-f**_format_file_name_  
  
> [!NOTE]  
> 비 XML 서식 파일을 구분하기 위해 파일 이름 확장명으로 .fmt를 사용하는 것이 좋습니다(예: MyTable.fmt).  
  
 비 XML 서식 파일의 구조 및 필드에 대한 자세한 내용은 [비 XML 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)에서 원래 지원했던 서식 파일입니다.  
  
### <a name="examples"></a>예  
 이 섹션에는 **bcp** 명령을 사용하여 비 XML 서식 파일을 만드는 방법을 보여 주는 다음 예가 포함되어 있습니다.  
  
-   A. 네이티브 데이터용 비 XML 서식 파일 만들기  
  
-   B. 문자 데이터용 비 XML 서식 파일 만들기  
  
-   C. 유니코드 네이티브 데이터용 비 XML 서식 파일 만들기  
  
-   D. 유니코드 문자 데이터용 비 XML 서식 파일 만들기  
  
-   F. 코드 페이지 옵션이 있는 형식 파일 사용  
  
 다음 예에서는 `HumanResources.Department` 예제 데이터베이스의 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 테이블을 사용합니다. `HumanResources.Department` 테이블에는 네 개의 열, 즉 `DepartmentID`, `Name`, `GroupName`및 `ModifiedDate`가 있습니다.  
  
#### <a name="a-creating-a-non-xml-format-file-for-native-data"></a>A. 네이티브 데이터용 비 XML 서식 파일 만들기  
 다음 예에서는 `Department-n.xml`테이블에 대한 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]`HumanResources.Department` XML 서식 파일을 만듭니다. 서식 파일은 네이티브 데이터 형식을 사용합니다. 생성된 서식 파일의 내용은 명령 뒤에 표시됩니다.  
  
 **bcp** 명령에는 다음 한정자가 포함됩니다.  
  
|한정자|Description|  
|----------------|-----------------|  
|**formatnul-f** _format_file_|비 XML 서식 파일을 지정합니다.|  
|**-n**|네이티브 데이터 형식을 지정합니다.|  
|**-T**|**bcp** 유틸리티가 통합 보안을 사용하는 트러스트된 연결을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 연결되도록 지정합니다. **-T** 를 지정하지 않은 경우 성공적으로 로그인하려면 **-U** 와 **-P** 를 지정해야 합니다.|  
  
 Windows 명령 프롬프트에 다음 `bcp` 명령을 입력합니다.  
  
```cmd
bcp AdventureWorks2012.HumanResources.Department format nul -T -n -f Department-n.fmt  
```  
  
 생성된 `Department-n.fmt`서식 파일에는 다음 정보가 포함됩니다.  
  
```  
12.0  
4  
1  SQLSMALLINT   0       2       ""   1     DepartmentID         ""  
2  SQLNCHAR      2       100     ""   2     Name                 SQL_Latin1_General_CP1_CI_AS  
3  SQLNCHAR      2       100     ""   3     GroupName            SQL_Latin1_General_CP1_CI_AS  
4  SQLDATETIME   0       8       ""   4     ModifiedDate         ""  
```  
  
 자세한 내용은 [비 XML 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)에서 원래 지원했던 서식 파일입니다.  
  
#### <a name="b-creating-a-non-xml-format-file-for-character-data"></a>B. 문자 데이터용 비 XML 서식 파일 만들기  
 다음 예에서는 `Department.fmt`테이블에 대한 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]`HumanResources.Department` XML 서식 파일을 만듭니다. 서식 파일은 문자 데이터 형식 및 기본이 아닌 필드 종결자(`,`)를 사용합니다. 생성된 서식 파일의 내용은 명령 뒤에 표시됩니다.  
  
 **bcp** 명령에는 다음 한정자가 포함됩니다.  
  
|한정자|Description|  
|----------------|-----------------|  
|**formatnul-f** _format_file_|비 XML 서식 파일을 지정합니다.|  
|**-c**|문자 데이터를 지정합니다.|  
|**-T**|**bcp** 유틸리티가 통합 보안을 사용하는 트러스트된 연결을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 연결되도록 지정합니다. **-T** 를 지정하지 않은 경우 성공적으로 로그인하려면 **-U** 와 **-P** 를 지정해야 합니다.|  
  
 Windows 명령 프롬프트에 다음 `bcp` 명령을 입력합니다.  
  
```cmd
bcp AdventureWorks2012.HumanResources.Department format nul -c -f Department-c.fmt -T  
```  
  
 생성된 `Department-c.fmt`서식 파일에는 다음 정보가 포함됩니다.  
  
```  
12.0  
4  
1  SQLCHAR       0       7       "\t"     1     DepartmentID            ""  
2  SQLCHAR       0       100     "\t"     2     Name                    SQL_Latin1_General_CP1_CI_AS  
3  SQLCHAR       0       100     "\t"     3     GroupName               SQL_Latin1_General_CP1_CI_AS  
4  SQLCHAR       0       24      "\r\n"   4     ModifiedDate            ""  
```  
  
 자세한 내용은 [비 XML 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)에서 원래 지원했던 서식 파일입니다.  
  
#### <a name="c-creating-a-non-xml-format-file-for-unicode-native-data"></a>C. 유니코드 네이티브 데이터용 비 XML 서식 파일 만들기  
 `HumanResources.Department` 테이블을 위한 유니코드 네이티브 데이터용 비 XML 서식 파일을 만들려면 다음 명령을 사용합니다.  
  
```cmd
bcp AdventureWorks2012.HumanResources.Department format nul -T -N -f Department-n.fmt  
```  
  
 유니코드 네이티브 데이터를 사용하는 방법에 대한 자세한 내용은 [데이터를 가져오거나 내보내기 위해 유니코드 네이티브 형식 사용&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)을 참조하세요.  
  
#### <a name="d-creating-a-non-xml-format-file-for-unicode-character-data"></a>D. 유니코드 문자 데이터용 비 XML 서식 파일 만들기  
 기본 종결자를 사용하는 `HumanResources.Department` 테이블을 위한 유니코드 문자 데이터용 비 XML 서식 파일을 만들려면 다음 명령을 사용합니다.  
  
```cmd
bcp AdventureWorks2012.HumanResources.Department format nul -T -w -f Department-w.fmt  
```  
  
 유니코드 문자 데이터를 사용하는 방법에 대한 자세한 내용은 [유니코드 문자 형식을 사용하여 데이터 가져오기 및 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)를 참조하세요.  
  
#### <a name="f-using-a-format-file-with-the-code-page-option"></a>F. 코드 페이지 옵션이 있는 형식 파일 사용  
bcp 명령을 사용하여 서식 파일을 만들 경우(즉, `bcp format` 사용), 데이터 정렬/코드 페이지에 대한 정보가 서식 파일에 기록됩니다.   
다음 예제에서는 열이 5개 있는 서식 파일에 데이터 정렬이 포함됩니다.  
  
```  
13.0  
5  
1  SQLCHAR         0       0       "**\t**"         1     c_0          Cyrillic_General_CS_AS  
2  SQLCHAR         0       0       "**\t**"         2     c_1          Cyrillic_General_CS_AS  
3  SQLCHAR         0       3000    "**\t**"         3     c_2          Cyrillic_General_CS_AS  
4  SQLCHAR         0       5       "**\t**"         4     c_3          ""  
5  SQLCHAR         0       41      "!!!\r\r\n"      5     c_4          ""  
  
```  
  
 `bcp in -c -C65001 -f format_file` ..." 또는 "`BULK INSERT`/`OPENROWSET` ... `FORMATFILE='format_file' CODEPAGE=65001` ..."을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 데이터를 가져오려는 경우 데이터 정렬/코드 페이지에 대한 정보가 65001 옵션보다 우선됩니다.  
따라서 서식 파일을 생성하는 경우 생성된 서식 파일에서 데이터 정렬 정보를 수동으로 삭제한 후 데이터 가져오기를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](으)로 다시 가져와야 합니다.  
다음은 데이터 정렬 정보가 없는 서식 파일의 예입니다.  
  
```  
13.0  
5  
1  SQLCHAR         0       0       "**\t**"         1     c_0              ""  
2  SQLCHAR         0       0       "**\t**"         2     c_1              ""  
3  SQLCHAR         0       3000    "**\t**"         3     c_2              ""  
4  SQLCHAR         0       5       "**\t**"         4     c_3              ""  
5  SQLCHAR         0       41      "!!!\r\r\n"      5     c_4              ""  
```  
  
## <a name="creating-an-xml-format-file"></a>XML 서식 파일 만들기  
 **bcp** 명령을 사용하여 서식 파일을 만들려면 데이터 파일 경로 대신 **format** 인수를 지정하고 **NUL** 을 사용합니다. 다음과 같이 **format** 옵션에는 항상 **-f** 옵션이 필요하며 XML 서식 파일을 만드는 경우 **-x** 옵션도 지정해야 합니다.  
  
 **bcp** _table_or_view_ **format nul-f** _format_file_name_ **-x**  
  
> [!NOTE]  
> XML 서식 파일을 구분하기 위해 파일 이름 확장명으로 .xml을 사용하는 것이 좋습니다(예: MyTable.xml).  
  
 XML 서식 파일의 구조 및 필드에 대한 자세한 내용은 [XML 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)에서 원래 지원했던 서식 파일입니다.  
  
### <a name="examples"></a>예  
 이 섹션에는 **bcp** 명령을 사용하여 XML 서식 파일을 만드는 방법을 보여 주는 다음 예가 포함되어 있습니다.  
  
-   A. 문자 데이터용 XML 서식 파일 만들기  
-   B. 네이티브 데이터용 XML 서식 파일 만들기  
  
 다음 예에서는 `HumanResources.Department` 예제 데이터베이스의 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 테이블을 사용합니다. `HumanResources.Department` 테이블에는 네 개의 열, 즉 `DepartmentID`, `Name`, `GroupName`및 `ModifiedDate`가 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssSampleDBdesc](../../includes/sssampledbdesc-md.md)]  
  
#### <a name="a-creating-an-xml-format-file-for-character-data"></a>A. 문자 데이터용 XML 서식 파일 만들기  
 다음 예에서는 `Department.xml`테이블에 대한 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]`HumanResources.Department` XML 서식 파일을 만듭니다. 서식 파일은 문자 데이터 형식 및 기본이 아닌 필드 종결자(`,`)를 사용합니다. 생성된 서식 파일의 내용은 명령 뒤에 표시됩니다.  
  
 **bcp** 명령에는 다음 한정자가 포함됩니다.  
  
|한정자|Description|  
|----------------|-----------------|  
|**formatnul-f** _format_file_ **-x**|XML 서식 파일을 지정합니다.|  
|**-c**|문자 데이터를 지정합니다.|  
|**-t** `,`|쉼표( **,** )를 필드 종결자로 지정합니다.<br /><br /> 참고: 데이터 파일이 기본 필드 종결자(`\t`)를 사용하면 **-t** 스위치는 불필요합니다.|  
|**-T**|**bcp** 유틸리티가 통합 보안을 사용하는 트러스트된 연결을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 연결되도록 지정합니다. **-T** 를 지정하지 않은 경우 성공적으로 로그인하려면 **-U** 와 **-P** 를 지정해야 합니다.|  
  
 Windows 명령 프롬프트에 다음 `bcp` 명령을 입력합니다.  
  
```cmd
bcp AdventureWorks2012.HumanResources.Department format nul -c -x -f Department-c.xml -t, -T  
```  
  
 생성된 `Department-c.xml`서식 파일에는 다음 XML 요소가 포함됩니다.  
  
```xml
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="24"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="DepartmentID" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Name" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="3" NAME="GroupName" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="ModifiedDate" xsi:type="SQLDATETIME"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
 이 서식 파일의 구문에 대한 자세한 내용은 [XML 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)을 참조하세요. 문자 데이터에 대한 자세한 내용은 [문자 형식을 사용하여 데이터 가져오기 및 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)를 참조하세요.  
  
#### <a name="b-creating-an-xml-format-file-for-native-data"></a>B. 네이티브 데이터용 XML 서식 파일 만들기  
 다음 예에서는 `Department-n.xml`테이블에 대한 `HumanResources.Department` XML 서식 파일을 만듭니다. 서식 파일은 네이티브 데이터 형식을 사용합니다. 생성된 서식 파일의 내용은 명령 뒤에 표시됩니다.  
  
 **bcp** 명령에는 다음 한정자가 포함됩니다.  
  
|한정자|Description|  
|----------------|-----------------|  
|**formatnul-f** _format_file_ **-x**|XML 서식 파일을 지정합니다.|  
|**-n**|네이티브 데이터 형식을 지정합니다.|  
|**-T**|**bcp** 유틸리티가 통합 보안을 사용하는 트러스트된 연결을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 연결되도록 지정합니다. **-T** 를 지정하지 않은 경우 성공적으로 로그인하려면 **-U** 와 **-P** 를 지정해야 합니다.|  
  
 Windows 명령 프롬프트에 다음 `bcp` 명령을 입력합니다.  
  
```cmd
bcp AdventureWorks2012.HumanResources.Department format nul -x -f Department-n.xml -n -T  
```  
  
 생성된 `Department-n.xml`서식 파일에는 다음 XML 요소가 포함됩니다.  
  
```xml
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="NativeFixed" LENGTH="2"/>  
  <FIELD ID="2" xsi:type="NCharPrefix" PREFIX_LENGTH="2" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="NCharPrefix" PREFIX_LENGTH="2" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="4" xsi:type="NativeFixed" LENGTH="8"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="DepartmentID" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Name" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="3" NAME="GroupName" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="ModifiedDate" xsi:type="SQLDATETIME"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
 이 서식 파일의 구문에 대한 자세한 내용은 [XML 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)을 참조하세요. 네이티브 데이터를 사용하는 방법에 대한 자세한 내용은 [네이티브 형식을 사용하여 데이터 가져오기 및 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)을 참조하세요.  
  
## <a name="mapping-data-fields-to-table-columns"></a>테이블 열에 데이터 필드 매핑  
 **bcp**에서 만든 서식 파일은 모든 테이블 열에 대한 설명을 순서대로 제공합니다. 서식 파일을 수정하여 테이블 행을 다시 정렬하거나 생략할 수 있습니다. 이렇게 하면 테이블 열에 직접 매핑하지 않는 필드가 있는 데이터 파일에 대해 서식 파일을 사용자 지정할 수 있습니다. 자세한 내용은 아래 항목을 참조하세요.  
  
-   [서식 파일을 사용하여 테이블 열 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [서식 파일을 사용하여 데이터 필드 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [bcp 유틸리티](../../tools/bcp-utility.md)   
 [서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)   
 [서식 파일을 사용하여 테이블 열 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [서식 파일을 사용하여 데이터 필드 건너뛰기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)   
 [비 XML 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)   
 [XML 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)  
  
  
