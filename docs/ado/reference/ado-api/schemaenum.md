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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4dd7edb2f5969f7ec8ded931c5e562c0c1992768
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47749231"
---
# <a name="schemaenum"></a>SchemaEnum
스키마의 유형을 지정 **레코드 집합** 하는 [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) 메서드 검색 합니다.  
  
## <a name="remarks"></a>Remarks  
 함수 및 열에 대 한 추가 정보가 반환 ADO 상수 각 항목에서 확인할 수 있습니다 [부록 b: 스키마 행 집합](http://msdn.microsoft.com/2b5fbf03-e50d-44ee-bc57-5a57666c55f1) OLE DB 프로그래머 참조입니다. 각 항목의 이름은 다음 표의 설명 섹션의 괄호 안에 나열 됩니다.  
  
 함수 및 열에 대 한 추가 정보가 반환 ADO MD 상수 각 항목에서 확인할 수 있습니다 [OLAP 개체 및 스키마 행 집합에 대 한 OLE DB](http://msdn.microsoft.com/d20bb2a6-68bd-423f-9ec8-eb930cd0c144) OLE DB에 대 한 분석 처리 OLAP (온라인) 설명서. 각 항목의 이름은 다음 표의 설명 열에 대 한 괄호 안에 나열 됩니다.  
  
 ADO의 설명을 참조 하 여 ADO 데이터 형식으로 OLE DB 설명서에 있는 열의 데이터 형식을 변환할 수 있습니다 [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) 항목입니다. 예를 들어을 OLE DB 데이터 형식 **DBTYPE_WSTR** 의 ADO 데이터 형식에 해당 **adWChar**합니다.  
  
 상수에 대 한 스키마 같은 결과 생성 하는 ADO **adSchemaDBInfoKeywords** 하 고 **adSchemaDBInfoLiterals**합니다. ADO 만듭니다는 **레코드 집합**, 후 각각 반환 하는 값을 사용 하 여 각 행을 채우는 합니다 **IDBInfo::GetKeywords** 및 **IDBInfo::GetLiteralInfo** 메서드. 이러한 메서드에 대 한 추가 정보를 찾을 수 있습니다 합니다 [IDBInfo](http://msdn.microsoft.com/3f5ad97f-3fc6-4f21-b691-f6911e4007f3) 는 OLE DB Programmer's Reference 부분입니다.  
  
|상수|값|Description|제약 조건 열|  
|--------------|-----------|-----------------|------------------------|  
|**adSchemaAsserts**|0|지정된 된 사용자가 소유 하는 카탈로그에 정의 된 어설션을 반환 합니다.<br /><br /> (어설션 행 집합)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCatalogs**|1|DBMS에서 액세스 가능한 카탈로그와 연결 된 실제 특성을 반환 합니다.<br /><br /> (카탈로그 행 집합)|CATALOG_NAME|  
|**adSchemaCharacterSets**|2|지정된 된 사용자에 액세스할 수 있는 카탈로그에 정의 된 문자 집합을 반환 합니다.<br /><br /> (CHARACTER_SETS 행 집합)|CHARACTER_SET_CATALOG CHARACTER_SET_SCHEMA CHARACTER_SET_NAME|  
|**adSchemaCheckConstraints**|5|Check 제약 조건 카탈로그에 정의 된 지정된 된 사용자가 소유한를 반환 합니다.<br /><br /> (CHECK_CONSTRAINTS) 행 집합)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCollations**|3|문자 데이터 정렬을 카탈로그에 정의 된 지정된 된 사용자에 액세스할 수 있는 반환 합니다.<br /><br /> (데이터 정렬은 행 집합)|COLLATION_CATALOG COLLATION_SCHEMA COLLATION_NAME|  
|**adSchemaColumnPrivileges**|13|사용자가 사용할 수 있거나 지정된 된 사용자가 승인한 카탈로그에 정의 된 테이블의 열에는 권한을 반환 합니다.<br /><br /> (COLUMN_PRIVILEGES 행 집합)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME GRANTOR GRANTEE|  
|**adSchemaColumns**|4|테이블 (뷰 포함)는 카탈로그에 정의 된 지정된 된 사용자에 액세스할 수 있는 열을 반환 합니다.<br /><br /> (COLUMNS 행 집합)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaColumnsDomainUsage**|11|지정된 된 사용자가 소유 하 고 카탈로그에 정의 된 도메인에 종속 되어 있는 카탈로그에 정의 된 열을 반환 합니다.<br /><br /> (COLUMN_DOMAIN_USAGE 행 집합)|DOMAIN_CATALOG DOMAIN_SCHEMA DOMAIN_NAME COLUMN_NAME|  
|**adSchemaConstraintColumnUsage**|6|참조 제약 조건, unique 제약 조건, check 제약 조건 및 어설션을 사용 하 고 카탈로그에 정의 된 지정된 된 사용자가 소유 하 고 열을 반환 합니다.<br /><br /> (CONSTRAINT_COLUMN_USAGE 행 집합)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaConstraintTableUsage**|7|참조 제약 조건, unique 제약 조건, check 제약 조건 및 어설션이 지정된 된 사용자가 소유 하 고 카탈로그에 정의에서 사용 되는 테이블을 반환 합니다.<br /><br /> (CONSTRAINT_TABLE_USAGE 행 집합)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaCubes**|32|스키마 (또는 카탈로그, 공급자 스키마를 지원 하지 않는 경우)에서 사용할 수 있는 큐브에 대 한 정보를 반환 합니다.<br /><br /> (큐브 행 집합 *)|CATALOG_NAME SCHEMA_NAME CUBE_NAME|  
|**adSchemaDBInfoKeywords**|30|공급자별 키워드 목록을 반환합니다.<br /><br /> (IDBInfo::GetKeywords)|\<없음 >|  
|**adSchemaDBInfoLiterals**|31|텍스트 명령에서 사용 되는 공급자 특정 리터럴의 목록을 반환 합니다.<br /><br /> (IDBInfo::GetLiteralInfo)|\<없음 >|  
|**adSchemaDimensions**|33|지정 된 큐브의 차원에 대 한 정보를 반환합니다. 각 차원에 한 행씩이 있습니다.<br /><br /> (차원 행 집합)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_NAME DIMENSION_UNIQUE_NAME|  
|**adSchemaForeignKeys**|27|지정된 된 사용자가 카탈로그에 정의 된 외래 키 열을 반환 합니다.<br /><br /> (FOREIGN_KEYS 행 집합)|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME FK_TABLE_CATALOG FK_TABLE_SCHEMA FK_TABLE_NAME|  
|**adSchemaHierarchies**|34|차원에 사용할 수 있는 계층에 대 한 정보를 반환합니다.<br /><br /> (계층 구조 행 집합)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_NAME HIERARCHY_UNIQUE_NAME|  
|**adSchemaIndexes**|12|지정된 된 사용자가 소유 하는 카탈로그에 정의 된 인덱스를 반환 합니다.<br /><br /> (인덱스 행 집합)|TABLE_CATALOG TABLE_SCHEMA INDEX_NAME 형식 TABLE_NAME|  
|**adSchemaKeyColumnUsage**|8|지정된 된 사용자가 키로 제한 되는 카탈로그에 정의 된 열을 반환 합니다.<br /><br /> (KEY_COLUMN_USAGE 행 집합)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaLevels**|35|차원에 사용할 수 있는 수준에 대 한 정보를 반환합니다.<br /><br /> (수준 행 집합)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_NAME LEVEL_UNIQUE_NAME|  
|**adSchemaMeasures**|36|사용 가능한 측정값에 대 한 정보를 반환합니다.<br /><br /> (측정값 행 집합)|CATALOG_NAME SCHEMA_NAME CUBE_NAME MEASURE_NAME MEASURE_UNIQUE_NAME|  
|**adSchemaMembers**|38|사용 가능한 구성원에 대 한 정보를 반환합니다.<br /><br /> (멤버 행 집합)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME LEVEL_NUMBER MEMBER_NAME MEMBER_UNIQUE_NAME MEMBER_CAPTION MEMBER_TYPE Tree 연산자입니다. 자세한 내용은 OLE DB에 대 한 분석 처리 OLAP (온라인) 참조 합니다.|  
|**adSchemaPrimaryKeys**|28|지정된 된 사용자가 카탈로그에 정의 된 기본 키 열을 반환 합니다.<br /><br /> (PRIMARY_KEYS 행 집합)|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME|  
|**adSchemaProcedureColumns**|29|프로시저가 반환한 행 집합의 열에 대한 정보를 반환합니다.<br /><br /> (PROCEDURE_COLUMNS 행 집합)|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME COLUMN_NAME|  
|**adSchemaProcedureParameters**|26|프로시저의 매개 변수와 반환 코드에 대한 정보를 반환합니다.<br /><br /> (PROCEDURE_PARAMETERS 행 집합)|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PARAMETER_NAME|  
|**adSchemaProcedures**|16|지정된 된 사용자가 소유 하는 카탈로그에 정의 된 프로시저를 반환 합니다.<br /><br /> (프로시저 행 집합)|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PROCEDURE_TYPE|  
|**adSchemaProperties**|37|차원의 각 수준에 대 한 사용 가능한 속성에 대 한 정보를 반환합니다.<br /><br /> (속성 행 집합)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME MEMBER_UNIQUE_NAME PROPERTY_TYPE PROPERTY_NAME|  
|**adSchemaProviderSpecific**|-1|공급자 자체 비표준 스키마 쿼리를 정의 하는 경우 사용 합니다.|\<특정 공급자 >|  
|**adSchemaProviderTypes**|22|데이터 공급자에서 지 원하는 기본 데이터 형식을 반환 합니다.<br /><br /> (PROVIDER_TYPES 행 집합)|DATA_TYPE BEST_MATCH|  
|**AdSchemaReferentialConstraints**|9|참조 제약 조건을 카탈로그에 정의 된 지정된 된 사용자가 소유한를 반환 합니다.<br /><br /> (REFERENTIAL_CONSTRAINTS 행 집합)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaSchemata**|17|지정된 된 사용자가 소유한 스키마 (데이터베이스 개체)를 반환 합니다.<br /><br /> (스키마 행 집합)|CATALOG_NAME SCHEMA_NAME SCHEMA_OWNER|  
|**adSchemaSQLLanguages**|18|규칙 수준, 옵션 및 카탈로그에 정의 된 SQL 구현 처리 데이터에서 지 원하는 언어를 반환 합니다.<br /><br /> (SQL_LANGUAGES 행 집합)|\<없음 >|  
|**adSchemaStatistics**|19|지정된 된 사용자가 소유 하는 카탈로그에 정의 된 통계를 반환 합니다.<br /><br /> (통계 행 집합)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaTableConstraints**|10|테이블 제약 조건 카탈로그에 정의 된 지정된 된 사용자가 소유한를 반환 합니다.<br /><br /> (TABLE_CONSTRAINTS 행 집합)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME CONSTRAINT_TYPE|  
|**adSchemaTablePrivileges**|14|사용자가 사용할 수 있거나 지정된 된 사용자가 승인한 카탈로그에 정의 된 테이블에는 권한을 반환 합니다.<br /><br /> (TABLE_PRIVILEGES 행 집합)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME GRANTOR GRANTEE|  
|**adSchemaTables**|20|테이블 (뷰 포함)는 카탈로그에 정의 된 지정된 된 사용자에 액세스할 수 있는 반환 합니다.<br /><br /> (테이블 행 집합)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
|**adSchemaTranslations**|21|지정된 된 사용자에 액세스할 수 있는 카탈로그에 정의 된 문자 변환을 반환 합니다.<br /><br /> (번역 행 집합)|TRANSLATION_CATALOG TRANSLATION_SCHEMA TRANSLATION_NAME|  
|**adSchemaTrustees**|39|나중에 사용하도록 예약되어 있습니다.||  
|**adSchemaUsagePrivileges**|15|가 사용할 수 있거나 지정된 된 사용자가 승인한 카탈로그에서 정의 하는 개체에 대 한 USAGE 권한을 반환 합니다.<br /><br /> (USAGE_PRIVILEGES 행 집합)|OBJECT_CATALOG OBJECT_SCHEMA OBJECT_NAME OBJECT_TYPE GRANTOR 피부 여자|  
|**adSchemaViewColumnUsage**|24|테이블을 볼, 카탈로그에서 정의 및 지정된 된 사용자가 소유 하 고 열을 반환 하는 것은 다릅니다.<br /><br /> (VIEW_COLUMN_USAGE 행 집합)|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
|**adSchemaViews**|23|지정된 된 사용자에 액세스할 수 있는 카탈로그에 정의 된 뷰를 반환 합니다.<br /><br /> (뷰 행 집합)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaViewTableUsage**|25|반환 테이블을 볼, 카탈로그에 정의 및 지정 된 사용자가 소유 하는 테이블에 따라 달라 집니다.<br /><br /> (VIEW_TABLE_USAGE 행 집합)|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.Schema.ASSERTS|  
|AdoEnums.Schema.CATALOGS|  
|AdoEnums.Schema.CHARACTERSETS|  
|AdoEnums.Schema.CHECKCONSTRAINTS|  
|AdoEnums.Schema.COLLATIONS|  
|AdoEnums.Schema.COLUMNPRIVILEGES|  
|AdoEnums.Schema.COLUMNS|  
|AdoEnums.Schema.COLUMNSDOMAINUSAGE|  
|AdoEnums.Schema.CONSTRAINTCOLUMNUSAGE|  
|AdoEnums.Schema.CONSTRAINTTABLEUSAGE|  
|AdoEnums.Schema.CUBES|  
|AdoEnums.Schema.DBINFOKEYWORDS|  
|AdoEnums.Schema.DBINFOLITERALS|  
|AdoEnums.Schema.DIMENSIONS|  
|AdoEnums.Schema.FOREIGNKEYS|  
|AdoEnums.Schema.HIERARCHIES|  
|AdoEnums.Schema.INDEXES|  
|AdoEnums.Schema.KEYCOLUMNUSAGE|  
|AdoEnums.Schema.LEVELS|  
|AdoEnums.Schema.MEASURES|  
|AdoEnums.Schema.MEMBERS|  
|AdoEnums.Schema.PRIMARYKEYS|  
|AdoEnums.Schema.PROCEDURECOLUMNS|  
|AdoEnums.Schema.PROCEDUREPARAMETERS|  
|AdoEnums.Schema.PROCEDURES|  
|AdoEnums.Schema.PROPERTIES|  
|AdoEnums.Schema.PROVIDERSPECIFIC|  
|AdoEnums.Schema.PROVIDERTYPES|  
|AdoEnums.Schema.REFERENTIALCONTRAINTS|  
|AdoEnums.Schema.SCHEMATA|  
|AdoEnums.Schema.SQLLANGUAGES|  
|AdoEnums.Schema.STATISTICS|  
|AdoEnums.Schema.TABLECONSTRAINTS|  
|AdoEnums.Schema.TABLEPRIVILEGES|  
|AdoEnums.Schema.TABLES|  
|AdoEnums.Schema.TRANSLATIONS|  
|AdoEnums.Schema.TRUSTEES|  
|AdoEnums.Schema.USAGEPRIVILEGES|  
|AdoEnums.Schema.VIEWCOLUMNUSAGE|  
|AdoEnums.Schema.VIEWS|  
|AdoEnums.Schema.VIEWTABLEUSAGE|  
  
## <a name="applies-to"></a>적용 대상  
 [OpenSchema 메서드](../../../ado/reference/ado-api/openschema-method.md)
