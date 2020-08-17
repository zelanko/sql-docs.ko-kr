---
description: sys.system_objects(Transact-SQL)
title: sys.system_objects (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.system_objects
- system_objects
- system_objects_TSQL
- sys.system_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_objects catalog view
ms.assetid: 069e9045-97f2-4463-8e8f-c73855f3ea0a
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 24f2f124ea4e3e80bb90425a3863225246984e65
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88375919"
---
# <a name="syssystem_objects-transact-sql"></a>sys.system_objects(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  에 포함 된 모든 스키마 범위 시스템 개체에 대해 하나의 행을 포함 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. 모든 시스템 개체는 sys 또는 INFORMATION_SCHEMA 스키마에 포함됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|name|**sysname**|개체 이름입니다.|  
|object_id|**int**|개체 ID입니다. 데이터베이스 내에서 고유합니다.|  
|principal_id|**int**|스키마 소유자와 다른 경우 개별 소유자의 ID입니다. 기본적으로 스키마에 포함된 개체는 스키마 소유자가 소유합니다. 그러나 소유권을 변경하는 ALTER AUTHORIZATION 문을 사용하여 다른 소유자를 지정할 수 있습니다.<br /><br /> 다른 개별 소유자가 없으면 NULL입니다.<br /><br /> 개체 형식이 다음 중 하나인 경우 NULL입니다.<br /><br /> C = CHECK 제약 조건<br /><br /> D = DEFAULT(제약 조건 또는 독립 실행형)<br /><br /> F = FOREIGN KEY 제약 조건<br /><br /> PK = PRIMARY KEY 제약 조건<br /><br /> R = 규칙 (이전 스타일, 독립 실행형)<br /><br /> TA = 어셈블리(CLR) 트리거<br /><br /> TR = SQL 트리거<br /><br /> UQ = UNIQUE 제약 조건|  
|schema_id|**int**|개체가 포함된 스키마의 ID입니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 포함된 모든 스키마 범위 시스템 개체에서 이 값은 항상 (schema_id('sys'), schema_id('INFORMATION_SCHEMA'))입니다.|  
|parent_object_id|**int**|이 개체가 속하는 개체의 ID입니다.<br /><br /> 0 = 자식 개체가 아닙니다.|  
|type|**char(2)**|개체 유형:<br /><br /> AF = 집계 함수(CLR)<br /><br /> C = CHECK 제약 조건<br /><br /> D = DEFAULT(제약 조건 또는 독립 실행형)<br /><br /> F = FOREIGN KEY 제약 조건<br /><br /> FN = SQL 스칼라 함수<br /><br /> FS = 어셈블리(CLR) 스칼라 함수<br /><br /> FT = 어셈블리(CLR) 테이블 반환 함수<br /><br /> IF = SQL 인라인 테이블 반환 함수<br /><br /> IT = 내부 테이블<br /><br /> P = SQL 저장 프로시저<br /><br /> PC = 어셈블리(CLR) 저장 프로시저<br /><br /> PG = 계획 지침<br /><br /> PK = PRIMARY KEY 제약 조건<br /><br /> R = 규칙 (이전 스타일, 독립 실행형)<br /><br /> RF = 복제 필터 프로시저<br /><br /> S = 시스템 기본 테이블<br /><br /> SN = 동의어<br /><br /> SQ = 서비스 큐<br /><br /> TA = 어셈블리(CLR) DML 트리거<br /><br /> TF = SQL 테이블 반환 함수<br /><br /> TR = SQL DML 트리거<br /><br /> TT = 테이블 유형<br /><br /> U = 테이블(사용자 정의)<br /><br /> UQ = UNIQUE 제약 조건<br /><br /> V = 뷰<br /><br /> X = 확장 저장 프로시저|  
|type_desc|**nvarchar(60)**|개체 형식에 대한 설명입니다. AGGREGATE_FUNCTION<br /><br /> CHECK_CONSTRAINT<br /><br /> DEFAULT_CONSTRAINT<br /><br /> FOREIGN_KEY_CONSTRAINT<br /><br /> SQL_SCALAR_FUNCTION<br /><br /> CLR_SCALAR_FUNCTION<br /><br /> CLR_TABLE_VALUED_FUNCTION<br /><br /> SQL_INLINE_TABLE_VALUED_FUNCTION<br /><br /> INTERNAL_TABLE<br /><br /> SQL_STORED_PROCEDURE<br /><br /> CLR_STORED_PROCEDURE<br /><br /> PLAN_GUIDE<br /><br /> PRIMARY_KEY_CONSTRAINT<br /><br /> RULE<br /><br /> REPLICATION_FILTER_PROCEDURE<br /><br /> SYSTEM_TABLE<br /><br /> SYNONYM<br /><br /> SERVICE_QUEUE<br /><br /> CLR_TRIGGER<br /><br /> SQL_TABLE_VALUED_FUNCTION<br /><br /> SQL_TRIGGER<br /><br /> TABLE_TYPE<br /><br /> USER_TABLE<br /><br /> UNIQUE_CONSTRAINT<br /><br /> VIEW<br /><br /> EXTENDED_STORED_PROCEDURE|  
|create_date|**datetime**|개체를 만든 날짜입니다.|  
|modify_date|**datetime**|ALTER 문을 사용하여 개체를 마지막으로 수정한 날짜입니다. 개체가 테이블이나 뷰인 경우 테이블이나 뷰에서 클러스터형 인덱스가 생성되거나 변경되면 modify_date도 변경됩니다.|  
|is_ms_shipped|**bit**|개체가 내부 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소로 만들어집니다.|  
|is_published|**bit**|개체가 게시됩니다.|  
|is_schema_published|**bit**|개체의 스키마만 게시됩니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
