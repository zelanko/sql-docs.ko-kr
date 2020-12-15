---
description: sys.table_types(Transact-SQL)
title: sys.table_types (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- table_types_TSQL
- sys.table_types
- sys.table_types_TSQL
- table_types
dev_langs:
- TSQL
helpviewer_keywords:
- table types [SQL Server]
- table-valued parameters, sys.table_types
- sys.table_types
- UDTT
ms.assetid: c05fd873-aff2-4a89-9936-a54c2ea09996
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0e55d33dbc18c8a06100a2ffab4b9ea3691aabc1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482884"
---
# <a name="systable_types-transact-sql"></a>sys.table_types(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자 정의 테이블 형식의 속성을 표시합니다. 테이블 형식은 테이블 변수 또는 테이블 반환 매개 변수를 선언하는 데 사용할 수 있는 형식입니다. 각 테이블 형식에는 [sys. objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) 카탈로그 뷰에 대 한 외래 키인 **type_table_object_id** 있습니다. 이 ID 열을 사용 하 여 일반 테이블의 **object_id** 열과 비슷한 방식으로 다양 한 카탈로그 뷰를 쿼리하여 해당 열과 제약 조건과 같은 테이블 형식의 구조를 검색할 수 있습니다.    
 
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|*\<inherited columns>*||이 뷰가 상속 하는 열 목록은 [sys. types &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)를 참조 하세요.|  
|**type_table_object_id**|**int**|개체 ID입니다. 데이터베이스 내에서 고유합니다.|  
|**is_memory_optimized**|**bit**|**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상<br /><br /> 가능한 값은 다음과 같습니다.<br /><br /> 0 = 메모리 최적화가 아닙니다.<br /><br /> 1 = 메모리 최적화입니다.<br /><br /> 0 값은 기본값입니다.<br /><br /> 테이블 형식은 항상 DURABILITY = SCHEMA_ONLY로 만들어집니다. 스키마만 디스크에 저장됩니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Table-Valued 매개 변수를 사용 하 여 데이터베이스 엔진 &#40;&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)   
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
