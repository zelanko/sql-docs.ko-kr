---
title: 인벤토리 스키마 (AccessToSQL)에 액세스 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
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
manager: craigg
ms.openlocfilehash: b0344fcfa5a5b174ef080a5eac431cebf6372842
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393711"
---
# <a name="access-inventory-schemas-accesstosql"></a>Access 인벤토리 스키마 (AccessToSQL)
다음 섹션에 액세스 하는 스키마를 내보낼 때 SSMA에서 만든 테이블에 설명 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
## <a name="databases"></a>데이터베이스  
데이터베이스 메타 데이터를 내보낸 합니다 **SSMA_Access_InventoryDatabases** 테이블입니다. 이 테이블에는 다음 열을 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|각 데이터베이스를 고유 하 게 식별 하는 GUID입니다. 이 열은 테이블에 대 한 기본 키 이기도합니다.|  
|**DatabaseName**|**nvarchar(4000)**|Access 데이터베이스의 이름입니다.|  
|**ExportTime**|**datetime**|날짜 및 SSMA 하 여이 메타 데이터를 만든 시간입니다.|  
|**파일 경로**|**nvarchar(4000)**|Access 데이터베이스의 전체 경로 및 파일 이름입니다.|  
|**FileSize**|**bigint**|기술 자료에서 Access 데이터베이스의 크기입니다.|  
|**FileOwner**|**nvarchar(4000)**|Access 데이터베이스의 소유자로 지정 된 Windows 계정입니다.|  
|**DateCreated**|**datetime**|날짜 및 Access 데이터베이스를 만든 시간입니다.|  
|**DateModified**|**datetime**|날짜 및 Access 데이터베이스를 마지막으로 수정한 시간입니다.|  
|**TablesCount**|**int**|Access 데이터베이스의 테이블 수입니다.|  
|**QueriesCount**|**int**|Access 데이터베이스의 쿼리 수입니다.|  
|**FormsCount**|**int**|Access 데이터베이스에서 폼의 수입니다.|  
|**ModulesCount**|**int**|액세스 데이터베이스에 있는 모듈의 수입니다.|  
|**ReportsCount**|**int**|Access 데이터베이스에서 보고서의 수입니다.|  
|**MacrosCount**|**int**|Access 데이터베이스에서 매크로의 수입니다.|  
|**AccessVersion**|**nvarchar(4000)**|액세스 데이터베이스의 버전입니다.|  
|**데이터 정렬**|**nvarchar(4000)**|Access 데이터베이스의 데이터 정렬입니다. 데이터 정렬은 데이터베이스 정렬 하 고 문자열을 비교 하는 방법을 결정 합니다.|  
|**JetVersion**|**nvarchar(4000)**|Jet 데이터베이스 엔진 버전입니다. Access 데이터베이스 내부 Jet 데이터베이스 엔진을 사용합니다.|  
|**IsUpdatable**|**bit**|데이터베이스를 업데이트할 수는 경우를 나타냅니다. 값이 1 이면 데이터베이스가 업데이트할 수 있습니다. 값이 0 이면 데이터베이스가 읽기 전용입니다.|  
|**QueryTimeout**|**int**|ODBC 쿼리 시간 제한의 구성된 값을 초 단위로 데이터베이스. 기본값은 60초입니다.|  
  
## <a name="tables"></a>테이블  
테이블 메타 데이터를 내보낸 합니다 **SSMA_Access_InventoryTables** 테이블입니다. 이 테이블에는 다음 열을 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|이 테이블을 포함 하는 데이터베이스를 식별 합니다.|  
|**TableId**|**uniqueidentifier**|테이블을 고유 하 게 식별 하는 GUID입니다. 이 열은 테이블에 대 한 기본 키 이기도합니다.|  
|**TableName**|**nvarchar(4000)**|테이블의 이름입니다.|  
|**RowsCount**|**int**|테이블의 행 수입니다.|  
|**ValidationRule**|**nvarchar(4000)**|테이블에 대 한 유효한 입력을 정의 하는 규칙입니다. 유효성 검사 규칙이 없으면 빈 문자열 필드에 포함 됩니다.|  
|**LinkedTable**|**nvarchar(4000)**|다른 테이블에 있는 경우 테이블을 사용 하 여 연결 된입니다. 테이블 연결이 테이블을 사용 하 여 추가, 삭제 및 다른 테이블에 업데이트 하면 됩니다.|  
|**ExternalSource**|**nvarchar(4000)**|데이터 원본에 있는 경우와 연결 된 테이블입니다. 테이블에 연결 하는 경우이 필드에 지정 된 외부 데이터 원본을 있습니다.|  
  
## <a name="columns"></a>열  
열 메타 데이터를 내보낸 합니다 **SSMA_Access_InventoryColumns** 테이블입니다. 이 테이블에는 다음 열을 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|이 열이 포함 된 데이터베이스를 식별 합니다.|  
|**TableId**|**uniqueidentifier**|이 열이 포함 된 테이블을 식별 합니다.|  
|**ColumnId**|**int**|열을 식별 하는 증분 정수입니다. **ColumnId** 테이블에 대 한 기본 키가 있습니다.|  
|**ColumnName**|**nvarchar(4000)**|열 이름입니다.|  
|**IsNullable**|**bit**|열 null 값에 대 한 경우를 지정 합니다. 값이 1 이면 열의 null 값을 포함할 수 있습니다. 값이 0 이면 열의 null 값을 포함할 수 없습니다. Null 값을 방지 하려면에 유효성 검사 규칙 데도 사용할 수 있습니다 note 합니다.|  
|**DataType**|**nvarchar(4000)**|데이터 액세스 등의 입력 열 **텍스트** 하거나 **긴**합니다.|  
|**IsAutoIncrement**|**bit**|정수 값 열이 자동으로 증가 하는 경우를 지정 합니다. 값이 1 이면 정수는 자동으로 증가 합니다.|  
|**Ordinal**|**smallint**|0부터 테이블의 열 순서입니다.|  
|**DefaultValue**|**nvarchar(4000)**|열의 기본값입니다.|  
|**ValidationRule**|**nvarchar(4000)**|열에서 업데이트 또는 추가할 데이터의 유효성을 검사 하는 데 사용 되는 규칙입니다.|  
  
## <a name="indexes"></a>인덱스  
인덱스 메타 데이터를 내보낸 합니다 **SSMA_Access_InventoryIndexes** 테이블입니다. 이 테이블에는 다음 열을 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|이 인덱스가 포함 된 데이터베이스를 식별 합니다.|  
|**TableId**|**uniqueidentifier**|이 인덱스를 포함 하는 테이블을 식별 합니다.|  
|**IndexId**|**int**|인덱스를 식별 하는 증분 정수입니다. 이 열은 테이블에 대 한 기본 키.|  
|**IndexName**|**nvarchar(4000)**|인덱스의 이름입니다.|  
|**ColumnsIncluded**|**nvarchar(4000)**|인덱스에 포함 된 열을 나열 합니다. 열 이름은 세미콜론으로 구분 됩니다.|  
|**IsUnique**|**bit**|인덱스의 각 항목 고유 해야 하는 경우를 지정 합니다. 다중 열 인덱스에 대해 값의 조합이 고유 해야 합니다. 값이 1 이면 인덱스는 고유 값을 적용 합니다.|  
|**IsPK**|**bit**|인덱스 기본 키 정의의 일부로 자동으로 생성 된 경우를 지정 합니다.|  
|**IsClustered**|**bit**|인덱스가 클러스터형 인지 하는 경우를 지정 합니다. 클러스터형된 인덱스 데이터의 물리적 저장소를 다시 정렬합니다. 테이블에 클러스터형된 인덱스가 하나만 있을 수 있습니다.|  
  
## <a name="foreign-keys"></a>외래 키  
외래 키 메타 데이터를 내보낸 합니다 **SSMA_Access_InventoryForeignKeys** 테이블입니다. 이 테이블에는 다음 열을 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|이 외래 키를 포함 하는 데이터베이스를 식별 합니다.|  
|**TableId**|**uniqueidentifier**|이 외래 키를 포함 하는 테이블을 식별 합니다.|  
|**ForeignKeyId**|**int**|외래 키를 식별 하는 증분 정수입니다. 이 열은 테이블에 대 한 기본 키.|  
|**ForeignKeyName**|**nvarchar(4000)**|인덱스의 이름입니다.|  
|**ReferencedTableId**|**uniqueidentifier**|원본 열이 포함 된 테이블을 식별 합니다.|  
|**SourceColumns**|**nvarchar(4000)**|외래 키 열 또는 열을 나열합니다.|  
|**ReferencedColumns**|**nvarchar(4000)**|기본 키 열 또는 외래 키에서 참조 되는 열을 나열 합니다.|  
|**IsCascadeForUpdate**|**bit**|기본 키 값이 업데이트 되 면 해당 키 값을 참조 하는 모든 행도 업데이트 됩니다 지정 합니다.|  
|**IsCascadeForDelete**|**bit**|기본 키 값을 삭제 하면 해당 키 값을 참조 하는 모든 행도 삭제 됩니다 지정 합니다.|  
|**IsEnforced**|**bit**|Foreign key 제약 조건을 적용 되도록 지정 합니다.|  
  
## <a name="queries"></a>쿼리  
쿼리 메타 데이터를 내보낸 합니다 **SSMA_Access_InventoryQueries** 테이블입니다. 이 테이블에는 다음 열을 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|이 쿼리를 포함 하는 데이터베이스를 식별 합니다.|  
|**QueryId**|**int**|쿼리를 식별 하는 증분 정수입니다. 이 열은 테이블에 대 한 기본 키.|  
|**QueryName**|**nvarchar(4000)**|쿼리의 이름입니다.|  
|**QueryText**|**nvarchar(4000)**|SELECT 문 처럼 표시 되는 SQL 쿼리 코드입니다.|  
|**IsUpdateable**|**bit**|업데이트 가능 또는 읽기 전용 쿼리 인지 여부를 지정 합니다.|  
|**QueryType**|**nvarchar(4000)**|와 같은 쿼리 유형을 지정 **선택** 하거나 **SetOperation**합니다.|  
|**ExternalSource**|**nvarchar(4000)**|쿼리가 외부 데이터 소스를 참조 하는 경우 쿼리에서 사용 되는 연결 문자열입니다.|  
  
## <a name="forms"></a>폼  
형식 메타 데이터를 내보낸 합니다 **SSMA_Access_InventoryForms** 테이블입니다. 이 테이블에는 다음 열을 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|이 양식을 포함 하는 데이터베이스를 식별 합니다.|  
|**FormId**|**int**|폼을 식별 하는 증분 정수입니다. 이 열은 테이블에 대 한 기본 키.|  
|**FormName**|**nvarchar(4000)**|양식의 이름입니다.|  
  
## <a name="macros"></a>매크로  
매크로 메타 데이터를 내보낸 합니다 **SSMA_Access_InventoryMacros** 테이블입니다. 이 테이블에는 다음 열을 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|매크로 포함 하는 데이터베이스를 식별 합니다.|  
|**MacroId**|**int**|매크로 식별 하는 증분 정수입니다. 이 열은 테이블에 대 한 기본 키.|  
|**MacroName**|**nvarchar(4000)**|매크로의 이름입니다.|  
  
## <a name="reports"></a>보고서  
로 내보낸 보고서 메타 데이터를 **SSMA_Access_InventoryReports** 테이블입니다. 이 테이블에는 다음 열을 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|보고서가 포함 된 데이터베이스를 식별 합니다.|  
|**ReportId**|**int**|보고서를 식별 하는 증분 정수입니다. 이 열은 테이블에 대 한 기본 키.|  
|**ReportName**|**nvarchar(4000)**|보고서의 이름|  
  
## <a name="modules"></a>모듈  
모듈 메타 데이터를 내보낸 합니다 **SSMA_Access_InventoryModules** 테이블입니다. 이 테이블에는 다음 열을 포함 합니다.  
  
|열 이름|데이터 형식|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|모듈을 포함 하는 데이터베이스를 식별 합니다.|  
|**ModuleId**|**int**|모듈을 식별 하는 증분 정수입니다. 이 열은 테이블에 대 한 기본 키.|  
|**ModuleName**|**nvarchar(4000)**|모듈의 이름입니다.|  
  
## <a name="see-also"></a>관련 항목  
[Access 인벤토리 내보내기](exporting-an-access-inventory-accesstosql.md)  
  
