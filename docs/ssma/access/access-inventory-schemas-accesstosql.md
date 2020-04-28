---
title: 액세스 인벤토리 스키마 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- columns table
- databases table
- exported metadata
- exporting, schemas of exported metadata
- foreign keys table
- forms table
- indexes, table
- inventory schemas
- macros table
- modules table
- queries table
- reference, inventory schemas
- reports table
- schemas of exported metadata
- schemas, exported metadata
- SSMA_Access_InventoryColumns
- SSMA_Access_InventoryDatabases
- SSMA_Access_InventoryForeignKeys
- SSMA_Access_InventoryForms
- SSMA_Access_InventoryIndexes
- SSMA_Access_InventoryMacros
- SSMA_Access_InventoryModules
- SSMA_Access_InventoryQueries
- SSMA_Access_InventoryReports
- SSMA_Access_InventoryTables
- tables, inventory
ms.assetid: fdd3cff2-4d62-4395-8acf-71ea8f17f524
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c140489877be5f34bc6d7a5b20a4ce36fdb3820f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68068952"
---
# <a name="access-inventory-schemas-accesstosql"></a>AccessToSQL (액세스 인벤토리 스키마)
다음 섹션에서는에 액세스 스키마를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]내보낼 때 ssma에서 만드는 테이블에 대해 설명 합니다.  
  
## <a name="databases"></a>데이터베이스  
데이터베이스 메타 데이터를 **SSMA_Access_InventoryDatabases** 테이블로 내보냅니다. 이 테이블에는 다음 열이 있습니다.  
  
|열 이름|데이터 형식|설명|  
|---------------|-------------|---------------|  
|**다르게**|**uniqueidentifier**|각 데이터베이스를 고유 하 게 식별 하는 GUID입니다. 이 열은 테이블의 기본 키 이기도 합니다.|  
|**DatabaseName**|**nvarchar(4000)**|액세스 데이터베이스의 이름입니다.|  
|**ExportTime**|**datetime**|SSMA에서이 메타 데이터를 만든 날짜와 시간입니다.|  
|**FilePath**|**nvarchar(4000)**|Access 데이터베이스의 전체 경로 및 파일 이름입니다.|  
|**FileSize**|**bigint**|액세스 데이터베이스의 크기 (KB)입니다.|  
|**FileOwner**|**nvarchar(4000)**|Access 데이터베이스의 소유자로 지정 된 Windows 계정입니다.|  
|**DateCreated**|**datetime**|액세스 데이터베이스를 만든 날짜와 시간입니다.|  
|**DateModified**|**datetime**|액세스 데이터베이스를 마지막으로 수정한 날짜와 시간입니다.|  
|**표 개수**|**int**|Access 데이터베이스의 테이블 수입니다.|  
|**QueriesCount**|**int**|Access 데이터베이스의 쿼리 수입니다.|  
|**FormsCount**|**int**|Access 데이터베이스의 폼 수입니다.|  
|**ModulesCount**|**int**|Access 데이터베이스의 모듈 수입니다.|  
|**ReportsCount**|**int**|Access 데이터베이스의 보고서 수입니다.|  
|**MacrosCount**|**int**|Access 데이터베이스의 매크로 수입니다.|  
|**AccessVersion**|**nvarchar(4000)**|데이터베이스의 액세스 버전입니다.|  
|**데이터 정렬**|**nvarchar(4000)**|Access 데이터베이스의 데이터 정렬입니다. 데이터 정렬은 데이터베이스에서 문자열을 정렬 하 고 비교 하는 방법을 결정 합니다.|  
|**JetVersion**|**nvarchar(4000)**|Jet 데이터베이스 엔진 버전입니다. Access 데이터베이스는 기본 Jet 데이터베이스 엔진을 사용 합니다.|  
|**IsUpdatable**|**bit**|데이터베이스를 업데이트할 수 있는지 여부를 나타냅니다. 값이 1 이면 데이터베이스를 업데이트할 수 있습니다. 값이 0 이면 데이터베이스가 읽기 전용입니다.|  
|**QueryTimeout**|**int**|데이터베이스에 대해 구성 된 ODBC 쿼리 제한 시간 값 (초)입니다. 기본값은 60초입니다.|  
  
## <a name="tables"></a>테이블  
테이블 메타 데이터를 **SSMA_Access_InventoryTables** 테이블로 내보냅니다. 이 테이블에는 다음 열이 있습니다.  
  
|열 이름|데이터 형식|설명|  
|---------------|-------------|---------------|  
|**다르게**|**uniqueidentifier**|이 테이블을 포함 하는 데이터베이스를 식별 합니다.|  
|**TableId**|**uniqueidentifier**|테이블을 고유 하 게 식별 하는 GUID입니다. 이 열은 테이블의 기본 키 이기도 합니다.|  
|**TableName**|**nvarchar(4000)**|테이블의 이름입니다.|  
|**RowsCount**|**int**|테이블의 행 수입니다.|  
|**ValidationRule**|**nvarchar(4000)**|테이블에 대 한 유효한 입력을 정의 하는 규칙입니다. 유효성 검사 규칙이 없으면 필드에 빈 문자열이 포함 됩니다.|  
|**LinkedTable**|**nvarchar(4000)**|테이블과 연결 된 다른 테이블 (있는 경우)입니다. 테이블을 연결 하면이 테이블을 사용 하 여 다른 테이블에 대 한 추가, 삭제 및 업데이트를 수행할 수 있습니다.|  
|**ExternalSource**|**nvarchar(4000)**|테이블에 연결 된 데이터 원본 (있는 경우)입니다. 테이블이 연결 된 경우이 필드에는 외부 데이터 원본이 지정 됩니다.|  
  
## <a name="columns"></a>열  
열 메타 데이터를 **SSMA_Access_InventoryColumns** 테이블로 내보냅니다. 이 테이블에는 다음 열이 있습니다.  
  
|열 이름|데이터 형식|설명|  
|---------------|-------------|---------------|  
|**다르게**|**uniqueidentifier**|이 열을 포함 하는 데이터베이스를 식별 합니다.|  
|**TableId**|**uniqueidentifier**|이 열이 포함 된 테이블을 식별 합니다.|  
|**ColumnId**|**int**|열을 식별 하는 증분 정수입니다. **ColumnId** 는 테이블의 기본 키입니다.|  
|**ColumnName**|**nvarchar(4000)**|열 이름입니다.|  
|**IsNullable**|**bit**|열에 null 값이 포함 될 수 있는지 여부를 지정 합니다. 값이 1 이면 열에 null 값이 포함 될 수 있습니다. 값이 0 이면 열은 null 값을 포함할 수 없습니다. 유효성 검사 규칙을 사용 하 여 null 값을 방지할 수도 있습니다.|  
|**DataType**|**nvarchar(4000)**|**Text** 또는 **Long**과 같은 열의 액세스 데이터 형식입니다.|  
|**IsAutoIncrement**|**bit**|열이 정수 값을 자동으로 증가 하는지 여부를 지정 합니다. 값이 1 이면 정수는 자동으로 증가 합니다.|  
|**Ordinal**|**smallint**|테이블에서 열 순서 (0부터 시작)입니다.|  
|**DefaultValue**|**nvarchar(4000)**|열의 기본값입니다.|  
|**ValidationRule**|**nvarchar(4000)**|열에 추가 되거나 업데이트 된 데이터의 유효성을 검사 하는 데 사용 되는 규칙입니다.|  
  
## <a name="indexes"></a>인덱스  
인덱스 메타 데이터를 **SSMA_Access_InventoryIndexes** 테이블로 내보냅니다. 이 테이블에는 다음 열이 있습니다.  
  
|열 이름|데이터 형식|설명|  
|---------------|-------------|---------------|  
|**다르게**|**uniqueidentifier**|이 인덱스를 포함 하는 데이터베이스를 식별 합니다.|  
|**TableId**|**uniqueidentifier**|이 인덱스를 포함 하는 테이블을 식별 합니다.|  
|**IndexId**|**int**|인덱스를 식별 하는 증분 정수입니다. 이 열은 테이블의 기본 키입니다.|  
|**IndexName**|**nvarchar(4000)**|인덱스의 이름입니다.|  
|**포함 된**|**nvarchar(4000)**|인덱스에 포함 된 열을 나열 합니다. 열 이름은 세미콜론으로 구분 됩니다.|  
|**IsUnique**|**bit**|인덱스의 각 항목이 고유 해야 하는지 여부를 지정 합니다. 다중 열 인덱스의 경우 값의 조합은 고유 해야 합니다. 값이 1 이면 인덱스에서 고유한 값을 적용 합니다.|  
|**IsPK**|**bit**|기본 키를 정의 하는 과정에서 자동으로 인덱스가 생성 되었는지 여부를 지정 합니다.|  
|**IsClustered**|**bit**|인덱스가 클러스터형 인지 여부를 지정 합니다. 클러스터형 인덱스는 데이터의 물리적 저장소 순서를 다시 정렬 합니다. 테이블에는 클러스터형 인덱스가 하나만 있을 수 있습니다.|  
  
## <a name="foreign-keys"></a>외래 키  
외래 키 메타 데이터를 **SSMA_Access_InventoryForeignKeys** 테이블로 내보냅니다. 이 테이블에는 다음 열이 있습니다.  
  
|열 이름|데이터 형식|설명|  
|---------------|-------------|---------------|  
|**다르게**|**uniqueidentifier**|이 외래 키를 포함 하는 데이터베이스를 식별 합니다.|  
|**TableId**|**uniqueidentifier**|이 외래 키가 포함 된 테이블을 식별 합니다.|  
|**ForeignKeyId**|**int**|외래 키를 식별 하는 증분 정수입니다. 이 열은 테이블의 기본 키입니다.|  
|**ForeignKeyName**|**nvarchar(4000)**|인덱스의 이름입니다.|  
|**ReferencedTableId**|**uniqueidentifier**|원본 열이 포함 된 테이블을 식별 합니다.|  
|**SourceColumns**|**nvarchar(4000)**|외래 키 열을 나열 합니다.|  
|**ReferencedColumns**|**nvarchar(4000)**|외래 키에서 참조 하는 기본 키 열을 나열 합니다.|  
|**IsCascadeForUpdate**|**bit**|기본 키 값이 업데이트 되 면 해당 키 값을 참조 하는 모든 행도 업데이트 되도록 지정 합니다.|  
|**IsCascadeForDelete**|**bit**|기본 키 값이 삭제 되 면 해당 키 값을 참조 하는 모든 행도 삭제 되도록 지정 합니다.|  
|**IsEnforced 적용**|**bit**|Foreign key 제약 조건을 적용 하도록 지정 합니다.|  
  
## <a name="queries"></a>쿼리  
쿼리 메타 데이터를 **SSMA_Access_InventoryQueries** 테이블로 내보냅니다. 이 테이블에는 다음 열이 있습니다.  
  
|열 이름|데이터 형식|설명|  
|---------------|-------------|---------------|  
|**다르게**|**uniqueidentifier**|이 쿼리를 포함 하는 데이터베이스를 식별 합니다.|  
|**QueryId**|**int**|쿼리를 식별 하는 증분 정수입니다. 이 열은 테이블의 기본 키입니다.|  
|**QueryName**|**nvarchar(4000)**|쿼리의 이름입니다.|  
|**QueryText**|**nvarchar(4000)**|SELECT 문과 같은 SQL 쿼리 코드입니다.|  
|**IsUpdateable**|**bit**|쿼리가 업데이트 가능한 또는 읽기 전용인 경우를 지정 합니다.|  
|**QueryType**|**nvarchar(4000)**|**Select** 또는 **SetOperation**와 같은 쿼리 유형을 지정 합니다.|  
|**ExternalSource**|**nvarchar(4000)**|쿼리가 외부 데이터 원본을 참조 하는 경우이는 쿼리에서 사용 하는 연결 문자열입니다.|  
  
## <a name="forms"></a>양식  
양식 메타 데이터를 **SSMA_Access_InventoryForms** 테이블로 내보냅니다. 이 테이블에는 다음 열이 있습니다.  
  
|열 이름|데이터 형식|설명|  
|---------------|-------------|---------------|  
|**다르게**|**uniqueidentifier**|이 폼을 포함 하는 데이터베이스를 식별 합니다.|  
|**FormId**|**int**|폼을 식별 하는 증분 정수입니다. 이 열은 테이블의 기본 키입니다.|  
|**FormName**|**nvarchar(4000)**|양식의 이름입니다.|  
  
## <a name="macros"></a>Macros  
매크로 메타 데이터를 **SSMA_Access_InventoryMacros** 테이블로 내보냅니다. 이 테이블에는 다음 열이 있습니다.  
  
|열 이름|데이터 형식|설명|  
|---------------|-------------|---------------|  
|**다르게**|**uniqueidentifier**|매크로를 포함 하는 데이터베이스를 식별 합니다.|  
|**MacroId**|**int**|매크로를 식별 하는 증분 정수입니다. 이 열은 테이블의 기본 키입니다.|  
|**사이의**|**nvarchar(4000)**|매크로 이름입니다.|  
  
## <a name="reports"></a>보고서  
보고서 메타 데이터를 **SSMA_Access_InventoryReports** 테이블로 내보냅니다. 이 테이블에는 다음 열이 있습니다.  
  
|열 이름|데이터 형식|설명|  
|---------------|-------------|---------------|  
|**다르게**|**uniqueidentifier**|보고서가 포함 된 데이터베이스를 식별 합니다.|  
|**보고서 id**|**int**|보고서를 식별 하는 증분 정수입니다. 이 열은 테이블의 기본 키입니다.|  
|**ReportName**|**nvarchar(4000)**|보고서의 이름|  
  
## <a name="modules"></a>모듈  
모듈 메타 데이터를 **SSMA_Access_InventoryModules** 테이블로 내보냅니다. 이 테이블에는 다음 열이 있습니다.  
  
|열 이름|데이터 형식|설명|  
|---------------|-------------|---------------|  
|**다르게**|**uniqueidentifier**|모듈을 포함 하는 데이터베이스를 식별 합니다.|  
|**ModuleId**|**int**|모듈을 식별 하는 증분 정수입니다. 이 열은 테이블의 기본 키입니다.|  
|**ModuleName**|**nvarchar(4000)**|모듈의 이름입니다.|  
  
## <a name="see-also"></a>참고 항목  
[Access 인벤토리 내보내기](exporting-an-access-inventory-accesstosql.md)  
  
