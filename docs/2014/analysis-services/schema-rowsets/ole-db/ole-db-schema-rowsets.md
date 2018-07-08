---
title: OLE DB 스키마 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
- apinav
helpviewer_keywords:
- schema rowsets [OLE DB]
- schema rowsets [Analysis Services], OLE DB
- OLE DB schema rowsets
- rowsets [Analysis Services], OLE DB
ms.assetid: ca2ee87a-ba04-4501-9125-33934c58ab31
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3a1d03d6fd8d527d48a9a4051f201368ff870882
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37161194"
---
# <a name="ole-db-schema-rowsets"></a>OLE DB 스키마 행 집합
  다음 OLE DB 스키마 행 집합은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XMLA(XML for Analysis) 공급자가 지원합니다. 사용 하 여는 `DISCOVER_ENUMERATORS` 포함 된 행 집합을 [검색](../../xmla/xml-elements-methods-discover.md) 특정 데이터 원본 공급자는 행 집합을 지원 하는지 여부를 확인 하는 메서드.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 웹 사이트에 있는 MSDN  Library의 OLE DB Programmer's Reference 부분에서 "Schema Rowsets" 항목을 검색하여 이러한 행 집합에 대한 자세한 정보를 찾을 수도 있습니다.  
  
 다음 표에서는 이 스키마 행 집합에 대해 설명합니다.  
  
|행 집합|Description|  
|------------|-----------------|  
|`DBSCHEMA_ASSERTIONS`|카탈로그에 정의되어 있고 지정된 사용자가 소유하고 있는 어설션을 식별합니다.|  
|[DBSCHEMA_CATALOGS 행 집합](dbschema-catalogs-rowset.md) <sup>1</sup>|DBMS(데이터베이스 관리 시스템)에서 액세스 가능한 카탈로그와 관련된 물리적 특성을 식별합니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Access와 같은 일부 시스템의 경우에는 카탈로그가 하나만 있을 수 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 경우 이 행 집합은 시스템 데이터베이스에 정의된 모든 카탈로그(데이터베이스)를 열거합니다.|  
|`DBSCHEMA_CHARACTER_SETS`|카탈로그에 정의되어 있고 지정된 사용자가 액세스할 수 있는 문자 집합을 식별합니다.|  
|`DBSCHEMA_CHECK_CONSTRAINTS`|카탈로그에 정의되어 있고 지정된 사용자가 소유하고 있는 CHECK 제약 조건을 식별합니다.|  
|`DBSCHEMA_CHECK_CONSTRAINTS_BY_TABLE`|지정된 사용자가 소유하고 있는 카탈로그에 정의된 지정된 테이블에 대한 CHECK 제약 조건을 식별합니다.|  
|`DBSCHEMA_COLLATIONS`|카탈로그에 정의되어 있고 지정된 사용자가 액세스할 수 있는 문자 데이터 정렬을 식별합니다.|  
|`DBSCHEMA_COLUMN_DOMAIN_USAGE`|카탈로그에 정의되어 있고 지정된 사용자가 소유하고 있는 도메인에 의존하는 카탈로그에 정의된 열을 식별합니다.|  
|`DBSCHEMA_COLUMN_PRIVILEGES`|지정된 사용자가 사용할 수 있거나 부여한 카탈로그에 정의된 테이블의 열에 대한 권한을 식별합니다.|  
|[DBSCHEMA_COLUMNS 행 집합](dbschema-columns-rowset.md) <sup>1</sup>|제공된 제한 조건을 충족하는 모든 열의 열 정보를 제공합니다.|  
|`DBSCHEMA_CONSTRAINT_COLUMN_USAGE`|카탈로그에 정의되어 있고 지정된 사용자가 소유하고 있는 참조 제약 조건, 고유 제약 조건, CHECK 제약 조건 및 어설션에서 사용하는 열을 식별합니다.|  
|`DBSCHEMA_CONSTRAINT_TABLE_USAGE`|카탈로그에 정의되어 있고 지정된 사용자가 소유하고 있는 참조 제약 조건, 고유 제약 조건, CHECK 제약 조건 및 어설션에서 사용하는 테이블을 식별합니다.|  
|`DBSCHEMA_FOREIGN_KEYS`|지정된 사용자가 카탈로그에 정의한 외래 키 열을 식별합니다. 이 스키마 행 집합은 SQL 이외 프로그래머의 편의를 위해 몇 가지 ISO 스키마 뷰를 기반으로 합니다. 지원되는 경우 이 스키마 행 집합은 관련된 ISO 뷰(`REFERENTIAL_CONSTRAINTS` 및 `CONSTRAINT_COLUMN_USAGE`)와 동기화되어야 합니다.|  
|`DBSCHEMA_INDEXES`|카탈로그에 정의되어 있고 지정된 사용자가 소유하고 있는 인덱스를 식별합니다.|  
|`DBSCHEMA_KEY_COLUMN_USAGE`|카탈로그에 정의되어 있고 지정된 사용자가 키로 제약하는 열을 식별합니다.|  
|`DBSCHEMA_PRIMARY_KEYS`|지정된 사용자가 카탈로그에 정의한 기본 키 열을 식별합니다. 이 스키마 행 집합은 SQL 이외 프로그래머의 편의를 위해 ISO 스키마 뷰를 기반으로 합니다. 지원되는 경우 이 스키마 행 집합은 관련된 ISO 뷰(`CONSTRAINT_COLUMN_USAGE`)와 동기화되어야 합니다.|  
|`DBSCHEMA_PROCEDURE_COLUMNS`|프로시저가 반환한 행 집합의 열에 대한 정보를 반환합니다.|  
|`DBSCHEMA_PROCEDURE_PARAMETERS`|프로시저의 매개 변수와 반환 코드에 대한 정보를 반환합니다.|  
|`DBSCHEMA_PROCEDURES`|카탈로그에 정의되어 있고 지정된 사용자가 소유하고 있는 프로시저를 식별합니다. 이는 OLE DB 확장입니다.|  
|[DBSCHEMA_PROVIDER_TYPES 행 집합](dbschema-provider-types-rowset.md) <sup>1</sup>|데이터 공급자가 지원하는 기본 데이터 형식을 식별합니다.|  
|`DBSCHEMA_REFERENTIAL_CONSTRAINTS`|카탈로그에 정의되어 있고 지정된 사용자가 소유하고 있는 참조 제약 조건을 식별합니다.|  
|`DBSCHEMA_SCHEMATA`|지정된 사용자가 소유하고 있는 스키마를 식별합니다.|  
|`DBSCHEMA_SQL_LANGUAGES`|카탈로그에 정의된 SQL 구현 처리 데이터의 지원을 받는 규칙 수준, 옵션 및 언어를 식별합니다.|  
|`DBSCHEMA_STATISTICS`|카탈로그에 정의되어 있고 지정된 사용자가 소유하고 있는 통계를 식별합니다.<br /><br /> 이 테이블은 `TABLE_STATISTICS` 행 집합과 관련이 없습니다.|  
|`DBSCHEMA_TABLE_CONSTRAINTS`|카탈로그에 정의되어 있고 지정된 사용자가 소유하고 있는 테이블 제약 조건을 식별합니다.|  
|`DBSCHEMA_TABLE_PRIVILEGES`|지정된 사용자가 사용할 수 있거나 부여한 카탈로그에 정의된 테이블에 대한 권한을 식별합니다.|  
|`DBSCHEMA_TABLE_STATISTICS`|공급자의 테이블에 대한 통계의 사용 가능한 집합을 설명합니다.<br /><br /> 이 행 집합은 `STATISTICS` 행 집합과 관련이 없습니다.|  
|[DBSCHEMA_TABLES 행 집합](dbschema-tables-rowset.md) <sup>1</sup>|측정값 그룹 및 차원을 내의 테이블로 표시 된 식별 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.|  
|`DBSCHEMA_TABLES_INFO` <sup>1</sup>|카탈로그에 정의되어 있고 지정된 사용자가 액세스할 수 있는 테이블(뷰 포함)을 식별합니다.|  
|`DBSCHEMA_TRANSLATIONS`|카탈로그에 정의되어 있고 지정된 사용자가 액세스할 수 있는 문자 변환을 식별합니다.|  
|`DBSCHEMA_TRUSTEE`|데이터 원본에 대한 트러스티를 열거합니다.|  
|`DBSCHEMA_USAGE_PRIVILEGES`|지정된 사용자가 사용할 수 있거나 부여한 카탈로그에 정의된 개체에 대한 `USAGE` 권한을 식별합니다.|  
|`DBSCHEMA_VIEW_COLUMN_USAGE`|카탈로그에 정의되어 있고 지정된 사용자가 액세스할 수 있는 뷰를 식별합니다.|  
|`DBSCHEMA_VIEW_TABLE_USAGE`|카탈로그에 정의되어 있고 지정된 사용자가 소유하고 있는 표시된 테이블이 의존하는 테이블을 식별합니다.|  
|`DBSCHEMA_VIEWS`|카탈로그에 정의되어 있고 지정된 사용자가 액세스할 수 있는 뷰를 식별합니다.|  
  
 <sup>1</sup> 용 MSOLAP 데이터 원본 공급자에서 지 원하는 스키마 행 집합을 나타냅니다는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XMLA 공급자입니다.  
  
## <a name="see-also"></a>관련 항목  
 [DISCOVER_ENUMERATORS 행 집합](../xml/discover-enumerators-rowset.md)   
 [Analysis Services 스키마 행 집합](../../schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
