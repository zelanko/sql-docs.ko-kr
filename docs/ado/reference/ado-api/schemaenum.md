---
title: SchemaEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SchemaEnum
helpviewer_keywords:
- SchemaEnum enumeration [ADO]
ms.assetid: 21c97651-297f-469f-b5b5-c48af72b62a8
author: rothja
ms.author: jroth
ms.openlocfilehash: cb004c33ae413c93506bc1c90b331494b7e56adc
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765434"
---
# <a name="schemaenum"></a>SchemaEnum
[OpenSchema](../../../ado/reference/ado-api/openschema-method.md) 메서드가 검색 하는 스키마 **레코드 집합** 의 유형을 지정 합니다.  
  
## <a name="remarks"></a>설명  
 각 ADO 상수에 대해 반환 되는 함수 및 열에 대 한 추가 정보는 부록 B: OLE DB 프로그래머 참조의 [스키마 행 집합](https://msdn.microsoft.com/2b5fbf03-e50d-44ee-bc57-5a57666c55f1) 에 있는 항목에서 찾을 수 있습니다. 각 항목의 이름은 다음 표의 설명 섹션에서 괄호 안에 나열 됩니다.  
  
 각 ADO MD 상수에 대해 반환 되는 함수 및 열에 대 한 추가 정보는 olap (온라인 분석 처리) 설명서에 대 한 OLE DB의 [Olap 개체 및 스키마 행 집합](https://msdn.microsoft.com/d20bb2a6-68bd-423f-9ec8-eb930cd0c144) 에 대 한 OLE DB 항목에서 찾을 수 있습니다. 각 항목의 이름은 다음 표의 설명 열에 괄호로 묶여 나열 됩니다.  
  
 ADO [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) 토픽의 Description 열을 참조 하 여 OLE DB 설명서에 있는 열의 데이터 형식을 ado 데이터 형식으로 변환할 수 있습니다. 예를 들어 **DBTYPE_WSTR** 의 OLE DB 데이터 형식은 **ADWCHAR**의 ADO 데이터 형식에 해당 합니다.  
  
 ADO는 상수, **Adschemadbinfokeywords** 및 **adSchemaDBInfoLiterals**에 대 한 스키마와 유사한 결과를 생성 합니다. ADO는 **레코드 집합**을 만든 다음 각 행을 **IDBInfo:: Getkeywords** 및 **IDBInfo:: GetLiteralInfo** 메서드에서 각각 반환 된 값으로 채웁니다. 이러한 메서드에 대 한 추가 정보는 OLE DB 프로그래머 참조의 [IDBInfo](https://msdn.microsoft.com/3f5ad97f-3fc6-4f21-b691-f6911e4007f3) 섹션에서 찾을 수 있습니다.  
  
|상수|값|설명|제약 조건 열|  
|--------------|-----------|-----------------|------------------------|  
|**adSchemaAsserts**|0|지정 된 사용자가 소유 하 고 있는 카탈로그에 정의 된 어설션을 반환 합니다.<br /><br /> (어설션 행 집합)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCatalogs**|1|DBMS에서 액세스할 수 있는 카탈로그에 연결 된 실제 특성을 반환 합니다.<br /><br /> (카탈로그 행 집합)|CATALOG_NAME|  
|**adSchemaCharacterSets**|2|지정 된 사용자가 액세스할 수 있는 카탈로그에 정의 된 문자 집합을 반환 합니다.<br /><br /> (CHARACTER_SETS 행 집합)|CHARACTER_SET_CATALOG CHARACTER_SET_SCHEMA CHARACTER_SET_NAME|  
|**adSchemaCheckConstraints**|5|지정 된 사용자가 소유 하 고 있는 카탈로그에 정의 된 check 제약 조건을 반환 합니다.<br /><br /> (CHECK_CONSTRAINTS) 집합|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCollations**|3|지정 된 사용자가 액세스할 수 있는 카탈로그에 정의 된 문자 데이터 정렬을 반환 합니다.<br /><br /> (데이터 정렬 행 집합)|COLLATION_CATALOG COLLATION_SCHEMA COLLATION_NAME|  
|**adSchemaColumnPrivileges**|13|지정 된 사용자가 사용할 수 있거나 지정 된 사용자가 부여한 카탈로그에 정의 된 테이블의 열에 대 한 권한을 반환 합니다.<br /><br /> (COLUMN_PRIVILEGES 행 집합)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME GRANTOR GRANTEE|  
|**adSchemaColumns**|4|지정 된 사용자가 액세스할 수 있는 카탈로그에 정의 된 테이블 (뷰 포함)의 열을 반환 합니다.<br /><br /> (열 행 집합)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaColumnsDomainUsage**|11|카탈로그에서 정의되고 지정된 사용자가 소유하고 있는 도메인에 의존하는 카탈로그에서 정의된 열을 반환합니다.<br /><br /> (COLUMN_DOMAIN_USAGE 행 집합)|DOMAIN_CATALOG DOMAIN_SCHEMA DOMAIN_NAME COLUMN_NAME|  
|**adSchemaConstraintColumnUsage**|6|카탈로그에서 정의되고 지정된 사용자가 소유하고 있는 참조 제약 조건, 고유 제약 조건, CHECK 제약 조건 그리고 어설션이 사용한 열을 반환합니다.<br /><br /> (CONSTRAINT_COLUMN_USAGE 행 집합)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaConstraintTableUsage**|7|카탈로그에서 정의되고 지정된 사용자가 소유하고 있는 참조 제약 조건, 고유 제약 조건, CHECK 제약 조건 그리고 어설션이 사용한 테이블을 반환합니다.<br /><br /> (CONSTRAINT_TABLE_USAGE 행 집합)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaCubes**|32|스키마 (또는 공급자가 스키마를 지원 하지 않는 경우 카탈로그)에서 사용 가능한 큐브에 대 한 정보를 반환 합니다.<br /><br /> (큐브 행 집합 *)|CATALOG_NAME SCHEMA_NAME CUBE_NAME|  
|**adSchemaDBInfoKeywords**|30|공급자별 키워드 목록을 반환합니다.<br /><br /> (IDBInfo:: GetKeywords)|\<없음>|  
|**adSchemaDBInfoLiterals**|31|텍스트 명령에서 사용된 공급자 특정 리터럴의 목록을 반환합니다.<br /><br /> (IDBInfo:: GetLiteralInfo)|\<없음>|  
|**adSchemaDimensions**|33|지정 된 큐브의 차원에 대 한 정보를 반환 합니다. 각 차원에 대해 행이 하나씩 있습니다.<br /><br /> (차원 행 집합)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_NAME DIMENSION_UNIQUE_NAME|  
|**adSchemaForeignKeys**|27|지정된 사용자가 카탈로그에서 정의한 외부 키 열을 반환합니다.<br /><br /> (FOREIGN_KEYS 행 집합)|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME FK_TABLE_CATALOG FK_TABLE_SCHEMA FK_TABLE_NAME|  
|**adSchemaHierarchies**|34|차원에서 사용할 수 있는 계층에 대 한 정보를 반환 합니다.<br /><br /> (계층 행 집합)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_NAME HIERARCHY_UNIQUE_NAME|  
|**adSchemaIndexes**|12|지정 된 사용자가 소유 하 고 있는 카탈로그에 정의 된 인덱스를 반환 합니다.<br /><br /> (인덱스 행 집합)|TABLE_CATALOG TABLE_SCHEMA INDEX_NAME 형식 TABLE_NAME|  
|**adSchemaKeyColumnUsage**|8|지정 된 사용자가 키로 제한 하는 카탈로그에 정의 된 열을 반환 합니다.<br /><br /> (KEY_COLUMN_USAGE 행 집합)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaLevels**|35|차원에서 사용할 수 있는 수준에 대 한 정보를 반환 합니다.<br /><br /> (수준 행 집합)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_NAME LEVEL_UNIQUE_NAME|  
|**adSchemaMeasures**|36|사용 가능한 측정값에 대 한 정보를 반환 합니다.<br /><br /> (측정값 행 집합)|CATALOG_NAME SCHEMA_NAME CUBE_NAME MEASURE_NAME MEASURE_UNIQUE_NAME|  
|**adSchemaMembers**|38|사용 가능한 멤버에 대 한 정보를 반환 합니다.<br /><br /> (멤버 행 집합)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME LEVEL_NUMBER MEMBER_NAME MEMBER_UNIQUE_NAME MEMBER_CAPTION MEMBER_TYPE 트리 연산자를 합니다. 자세한 내용은 OLAP (온라인 분석 처리)에 대 한 OLE DB를 참조 하세요.|  
|**adSchemaPrimaryKeys**|28|지정된 사용자가 카탈로그에서 정의한 기본 키 열을 반환합니다.<br /><br /> (PRIMARY_KEYS 행 집합)|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME|  
|**adSchemaProcedureColumns**|29|프로시저가 반환한 행 집합의 열에 대한 정보를 반환합니다.<br /><br /> (PROCEDURE_COLUMNS 행 집합)|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME COLUMN_NAME|  
|**adSchemaProcedureParameters**|26|프로시저의 매개 변수와 반환 코드에 대한 정보를 반환합니다.<br /><br /> (PROCEDURE_PARAMETERS 행 집합)|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PARAMETER_NAME|  
|**adSchemaProcedures**|16|지정 된 사용자가 소유 하 고 있는 카탈로그에 정의 된 프로시저를 반환 합니다.<br /><br /> (프로시저 행 집합)|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PROCEDURE_TYPE|  
|**adSchemaProperties**|37|차원의 각 수준에 대해 사용 가능한 속성에 대 한 정보를 반환 합니다.<br /><br /> (속성 행 집합)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME MEMBER_UNIQUE_NAME PROPERTY_TYPE PROPERTY_NAME|  
|**adSchemaProviderSpecific**|-1|공급자가 자체 비표준 스키마 쿼리를 정의 하는 경우 사용 됩니다.|\<공급자별>|  
|**adSchemaProviderTypes**|22|데이터 공급자가 지 원하는 (기본) 데이터 형식을 반환 합니다.<br /><br /> (PROVIDER_TYPES 행 집합)|DATA_TYPE BEST_MATCH|  
|**AdSchemaReferentialConstraints**|9|지정 된 사용자가 소유 하 고 있는 카탈로그에 정의 된 참조 제약 조건을 반환 합니다.<br /><br /> (REFERENTIAL_CONSTRAINTS 행 집합)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaSchemata**|17|지정 된 사용자가 소유 하 고 있는 스키마 (데이터베이스 개체)를 반환 합니다.<br /><br /> (SCHEMATA 행 집합)|CATALOG_NAME SCHEMA_NAME SCHEMA_OWNER|  
|**adSchemaSQLLanguages**|18|카탈로그에서 정의된 SQL-구현 처리 데이터의 지원을 받는 규칙 수준, 옵션 그리고 언어를 반환합니다.<br /><br /> (SQL_LANGUAGES 행 집합)|\<없음>|  
|**adSchemaStatistics**|19|지정 된 사용자가 소유 하 고 있는 카탈로그에 정의 된 통계를 반환 합니다.<br /><br /> (통계 행 집합)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaTableConstraints**|10|지정 된 사용자가 소유 하 고 있는 카탈로그에 정의 된 테이블 제약 조건을 반환 합니다.<br /><br /> (TABLE_CONSTRAINTS 행 집합)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME CONSTRAINT_TYPE|  
|**adSchemaTablePrivileges**|14|지정된 사용자가 사용할 수 있거나 지정된 사용자가 승인한 카탈로그에 정의된 테이블에 대한 권한을 반환합니다.<br /><br /> (TABLE_PRIVILEGES 행 집합)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME GRANTOR GRANTEE|  
|**adSchemaTables**|20|지정된 사용자가 액세스할 수 있는 카탈로그에 정의된 테이블(뷰 포함)을 반환합니다.<br /><br /> (테이블 행 집합)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
|**adSchemaTranslations**|21|지정 된 사용자가 액세스할 수 있는 카탈로그에 정의 된 문자 번역을 반환 합니다.<br /><br /> (번역 행 집합)|TRANSLATION_CATALOG TRANSLATION_SCHEMA TRANSLATION_NAME|  
|**adSchemaTrustees**|39|다음에 사용하도록 예약됩니다.||  
|**adSchemaUsagePrivileges**|15|지정 된 사용자가 사용할 수 있거나 지정 된 사용자가 부여한 카탈로그에 정의 된 개체에 대 한 사용 권한을 반환 합니다.<br /><br /> (USAGE_PRIVILEGES 행 집합)|OBJECT_CATALOG OBJECT_SCHEMA OBJECT_NAME OBJECT_TYPE GRANTOR 피부 여자|  
|**adSchemaViewColumnUsage**|24|카탈로그에 정의 되어 있고 지정 된 사용자가 소유 하 고 있는 표시 된 테이블이 종속 되는 열을 반환 합니다.<br /><br /> (VIEW_COLUMN_USAGE 행 집합)|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
|**adSchemaViews**|23|지정 된 사용자가 액세스할 수 있는 카탈로그에 정의 된 뷰를 반환 합니다.<br /><br /> (뷰 행 집합)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaViewTableUsage**|25|카탈로그에서 정의되고 지정된 사용자가 소유하고 있는 표시된 테이블이 의존하는 테이블을 반환합니다.<br /><br /> (VIEW_TABLE_USAGE 행 집합)|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums CHARACTERSETS|  
|AdoEnums 제약 조건|  
|AdoEnums|  
|AdoEnums 권한|  
|AdoEnums|  
|AdoEnums DOMAINUSAGE|  
|AdoEnums CONSTRAINTCOLUMNUSAGE|  
|AdoEnums CONSTRAINTTABLEUSAGE|  
|AdoEnums|  
|AdoEnums. 스키마.|  
|AdoEnums DBINFOLITERALS|  
|AdoEnums|  
|AdoEnums FOREIGNKEYS|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums. KEYCOLUMNUSAGE|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums 키|  
|AdoEnums PROCEDURECOLUMNS|  
|AdoEnums PROCEDUREPARAMETERS|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums REFERENTIALCONTRAINTS|  
|AdoEnums SCHEMATA|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums TABLECONSTRAINTS|  
|AdoEnums 권한|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums USAGEPRIVILEGES|  
|AdoEnums. VIEWCOLUMNUSAGE|  
|AdoEnums|  
|AdoEnums. VIEWTABLEUSAGE|  
  
## <a name="applies-to"></a>적용 대상  
 [OpenSchema 메서드](../../../ado/reference/ado-api/openschema-method.md)
