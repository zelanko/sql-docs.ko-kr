---
title: "인벤토리 스키마 (AccessToSQL) 액세스 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: "17"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d22835bef06693ecf2fef51240f4bd9d9607a8e0
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="access-inventory-schemas-accesstosql"></a>액세스 인벤토리 스키마 (AccessToSQL)
다음 섹션에서는 액세스 스키마를 내보낼 때 SSMA가 만든 테이블에 설명 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
## <a name="databases"></a>데이터베이스  
데이터베이스 메타 데이터가 내보내집니다는 **SSMA_Access_InventoryDatabases** 테이블입니다. 이 테이블 다음 열을 있습니다.  
  
|열 이름|데이터 형식|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|각 데이터베이스를 고유 하 게 식별 하는 GUID입니다. 이 열은 테이블에 대 한 기본 키 이기도합니다.|  
|**DatabaseName**|**nvarchar(4000)**|Access 데이터베이스의 이름입니다.|  
|**ExportTime**|**datetime**|날짜 및 SSMA 하 여이 메타 데이터를 만든 시간입니다.|  
|**파일 경로**|**nvarchar(4000)**|Access 데이터베이스의 전체 경로 및 파일 이름입니다.|  
|**파일 크기**|**bigint**|Kb에서 Access 데이터베이스의 크기입니다.|  
|**FileOwner**|**nvarchar(4000)**|Access 데이터베이스의 소유자로 지정 된 Windows 계정입니다.|  
|**DateCreated**|**datetime**|날짜 및 Access 데이터베이스를 만든 시간입니다.|  
|**DateModified**|**datetime**|날짜 및 Access 데이터베이스를 마지막으로 수정한 시간입니다.|  
|**TablesCount**|**int**|Access 데이터베이스의 테이블 수입니다.|  
|**QueriesCount**|**int**|Access 데이터베이스의 쿼리 수입니다.|  
|**FormsCount**|**int**|Access 데이터베이스에서 폼의 수입니다.|  
|**ModulesCount**|**int**|Access 데이터베이스에는 모듈 수입니다.|  
|**ReportsCount**|**int**|Access 데이터베이스에서 보고서의 수입니다.|  
|**MacrosCount**|**int**|Access 데이터베이스에 매크로의 수입니다.|  
|**AccessVersion**|**nvarchar(4000)**|데이터베이스의 액세스 버전입니다.|  
|**데이터 정렬**|**nvarchar(4000)**|Access 데이터베이스의 데이터 정렬입니다. 데이터 정렬은 데이터베이스 정렬 하 고 문자열을 비교 하는 방법을 결정 합니다.|  
|**JetVersion**|**nvarchar(4000)**|Jet 데이터베이스 엔진 버전입니다. Access 데이터베이스 기본 Jet 데이터베이스 엔진을 사용합니다.|  
|**IsUpdatable**|**bit**|데이터베이스를 업데이트할 수는 경우를 나타냅니다. 값이 1 이면 데이터베이스가 업데이트할 수 있습니다. 값이 0 이면 데이터베이스는 읽기 전용입니다.|  
|**쿼리 제한 시간**|**int**|구성 된 ODBC 쿼리 제한 시간 값 (초)에서 데이터베이스에 대 한 합니다. 기본값은 60초입니다.|  
  
## <a name="tables"></a>테이블  
테이블 메타 데이터가 내보내집니다는 **SSMA_Access_InventoryTables** 테이블입니다. 이 테이블 다음 열을 있습니다.  
  
|열 이름|데이터 형식|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|이 테이블을 포함 하는 데이터베이스를 식별 합니다.|  
|**TableId**|**uniqueidentifier**|테이블을 고유 하 게 식별 하는 GUID입니다. 이 열은 테이블에 대 한 기본 키 이기도합니다.|  
|**테이블 이름**|**nvarchar(4000)**|테이블의 이름입니다.|  
|**RowsCount**|**int**|테이블의 행 수입니다.|  
|**유효성 검사 규칙**|**nvarchar(4000)**|테이블에 대 한 유효한 입력을 정의 하는 규칙입니다. 유효성 검사 규칙이 없으면 빈 문자열 필드에 포함 됩니다.|  
|**LinkedTable**|**nvarchar(4000)**|다른, 있는 경우 연결 된 테이블을 테이블입니다. 이 테이블을 사용 하 여 추가, 삭제 및 다른 테이블에 대 한 업데이트를 허용 테이블을 연결 합니다.|  
|**ExternalSource**|**nvarchar(4000)**|데이터 원본에 있는 경우와 연결 된 테이블입니다. 테이블을 연결 하는 경우이 필드에 지정 된 외부 데이터 원본을 있습니다.|  
  
## <a name="columns"></a>열  
열 메타 데이터가 내보내집니다는 **SSMA_Access_InventoryColumns** 테이블입니다. 이 테이블 다음 열을 있습니다.  
  
|열 이름|데이터 형식|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|이 열이 포함 된 데이터베이스를 식별 합니다.|  
|**TableId**|**uniqueidentifier**|이 열이 포함 된 테이블을 식별 합니다.|  
|**ColumnId**|**int**|열을 식별 하는 증분 정수입니다. **ColumnId** 테이블에 대 한 기본 키가 있습니다.|  
|**ColumnName**|**nvarchar(4000)**|열 이름입니다.|  
|**IsNullable**|**bit**|열 null 값이 있으면 수를 지정 합니다. 값이 1 이면 열에 null 값 포함 될 수 있습니다. 값이 0 이면 열 null 값을 포함할 수 없습니다. Note null 값을 방지 하려면에 유효성 검사 규칙 데도 사용할 수 있습니다.|  
|**DataType**|**nvarchar(4000)**|열에서 데이터 액세스와 같은 유형의 **텍스트** 또는 **긴**합니다.|  
|**IsAutoIncrement**|**bit**|해당 열 정수 값이 자동으로 증가 하는 경우를 지정 합니다. 값이 1 이면 정수가 자동으로 증가 됩니다.|  
|**Ordinal**|**smallint**|0부터 시작 하는 테이블에 있는 열의 순서입니다.|  
|**DefaultValue**|**nvarchar(4000)**|열에 대 한 기본값입니다.|  
|**유효성 검사 규칙**|**nvarchar(4000)**|추가 하거나 업데이트할 열에서 데이터 유효성을 검사 하는 데 사용 되는 규칙입니다.|  
  
## <a name="indexes"></a>인덱스  
인덱스 메타 데이터가 내보내집니다는 **SSMA_Access_InventoryIndexes** 테이블입니다. 이 테이블 다음 열을 있습니다.  
  
|열 이름|데이터 형식|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|이 인덱스가 포함 된 데이터베이스를 식별 합니다.|  
|**TableId**|**uniqueidentifier**|이 인덱스를 포함 하는 테이블을 식별 합니다.|  
|**IndexId**|**int**|인덱스를 식별 하는 증분 정수입니다. 이 열은 테이블에 대 한 기본 키입니다.|  
|**IndexName**|**nvarchar(4000)**|인덱스의 이름입니다.|  
|**ColumnsIncluded**|**nvarchar(4000)**|인덱스에 포함 된 열을 나열 합니다. 열 이름은 세미콜론으로 구분 됩니다.|  
|**IsUnique**|**bit**|각 항목의 인덱스를 고유 해야 하는 경우를 지정 합니다. 다중 열 인덱스에서 값의 조합이 고유 해야 합니다. 값이 1 이면 인덱스는 고유 값을 적용 합니다.|  
|**IsPK**|**bit**|인덱스가 기본 키 정의의 일부로 자동으로 생성 하는 경우를 지정 합니다.|  
|**IsClustered**|**bit**|인덱스가 클러스터형 인지 하는 경우를 지정 합니다. 클러스터형된 인덱스는 데이터의 물리적 저장소를 다시 정렬합니다. 테이블에 클러스터형된 인덱스가 하나만 있을 수 있습니다.|  
  
## <a name="foreign-keys"></a>외래 키  
외래 키 메타 데이터를 내보낸는 **SSMA_Access_InventoryForeignKeys** 테이블입니다. 이 테이블 다음 열을 있습니다.  
  
|열 이름|데이터 형식|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|이 외래 키를 포함 하는 데이터베이스를 식별 합니다.|  
|**TableId**|**uniqueidentifier**|이 외래 키를 포함 하는 테이블을 식별 합니다.|  
|**ForeignKeyId**|**int**|외래 키를 식별 하는 증분 정수입니다. 이 열은 테이블에 대 한 기본 키입니다.|  
|**ForeignKeyName**|**nvarchar(4000)**|인덱스의 이름입니다.|  
|**ReferencedTableId**|**uniqueidentifier**|원본 열을 포함 하는 테이블을 식별 합니다.|  
|**SourceColumns**|**nvarchar(4000)**|외래 키 열 또는 열을 나열합니다.|  
|**ReferencedColumns**|**nvarchar(4000)**|기본 키 열 또는 외래 키에서 참조 된 열을 나열 합니다.|  
|**IsCascadeForUpdate**|**bit**|기본 키 값을 업데이트 하는 경우 해당 키 값을 참조 하는 모든 행도 업데이트 된을 지정 합니다.|  
|**IsCascadeForDelete**|**bit**|기본 키 값을 삭제 하면 해당 키 값을 참조 하는 모든 행도 삭제 됩니다 지정 합니다.|  
|**IsEnforced**|**bit**|외래 키 제약 조건을 적용 되는지 지정 합니다.|  
  
## <a name="queries"></a>쿼리  
쿼리 메타 데이터를 내보낸는 **SSMA_Access_InventoryQueries** 테이블입니다. 이 테이블 다음 열을 있습니다.  
  
|열 이름|데이터 형식|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|이 쿼리를 포함 하는 데이터베이스를 식별 합니다.|  
|**QueryId**|**int**|쿼리를 식별 하는 증분 정수입니다. 이 열은 테이블에 대 한 기본 키입니다.|  
|**쿼리 이름**|**nvarchar(4000)**|쿼리의 이름입니다.|  
|**QueryText**|**nvarchar(4000)**|SELECT 문 처럼 표시 되는 SQL 쿼리 코드입니다.|  
|**IsUpdateable**|**bit**|업데이트 가능 하거나 읽기 전용 쿼리 인지 여부를 지정 합니다.|  
|**QueryType**|**nvarchar(4000)**|와 같은 쿼리 유형을 지정 **선택** 또는 **SetOperation**합니다.|  
|**ExternalSource**|**nvarchar(4000)**|쿼리가 외부 데이터 소스를 참조 하는 경우 쿼리에 사용 된 연결 문자열입니다.|  
  
## <a name="forms"></a>양식  
양식 메타 데이터가 내보내집니다는 **SSMA_Access_InventoryForms** 테이블입니다. 이 테이블 다음 열을 있습니다.  
  
|열 이름|데이터 형식|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|이 폼이 포함 된 데이터베이스를 식별 합니다.|  
|**FormId**|**int**|폼을 식별 하는 증분 정수입니다. 이 열은 테이블에 대 한 기본 키입니다.|  
|**생략**|**nvarchar(4000)**|양식의 이름입니다.|  
  
## <a name="macros"></a>매크로  
매크로 메타 데이터가 내보내집니다는 **SSMA_Access_InventoryMacros** 테이블입니다. 이 테이블 다음 열을 있습니다.  
  
|열 이름|데이터 형식|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|매크로 포함 하는 데이터베이스를 식별 합니다.|  
|**MacroId**|**int**|매크로 식별 하는 증분 정수입니다. 이 열은 테이블에 대 한 기본 키입니다.|  
|**매크로 이름**|**nvarchar(4000)**|매크로의 이름입니다.|  
  
## <a name="reports"></a>보고서  
내보낸 보고서 메타 데이터는 **SSMA_Access_InventoryReports** 테이블입니다. 이 테이블 다음 열을 있습니다.  
  
|열 이름|데이터 형식|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|보고서가 포함 된 데이터베이스를 식별 합니다.|  
|**ReportId**|**int**|보고서를 식별 하는 증분 정수입니다. 이 열은 테이블에 대 한 기본 키입니다.|  
|**ReportName**|**nvarchar(4000)**|보고서의 이름|  
  
## <a name="modules"></a>모듈  
내보낼 모듈 메타 데이터는 **SSMA_Access_InventoryModules** 테이블입니다. 이 테이블 다음 열을 있습니다.  
  
|열 이름|데이터 형식|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|모듈을 포함 하는 데이터베이스를 식별 합니다.|  
|**모듈 Id**|**int**|모듈을 식별 하는 증분 정수입니다. 이 열은 테이블에 대 한 기본 키입니다.|  
|**모듈 이름**|**nvarchar(4000)**|모듈의 이름입니다.|  
  
## <a name="see-also"></a>관련 항목:  
[Access 인벤토리 내보내기](http://msdn.microsoft.com/en-us/7e1941fb-3d14-4265-aff6-c77a4026d0ed)  
  
