---
title: sys.sql_dependencies (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sql_dependencies
- sql_dependencies_TSQL
- sys.sql_dependencies_TSQL
- sys.sql_dependencies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_dependencies catalog view
ms.assetid: 1779aa87-a0b8-470a-a286-d7cc0b93ad2e
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bd2ad747dc3e9784a27e251193e789eabccae2f7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="syssqldependencies-transact-sql"></a>sys.sql_dependencies(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] 식에서 참조된 엔터티 또는 다른 개체로의 참조가 정의된 문의 종속성당 한 개의 행을 포함합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 사용 하 여 [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) 대신 합니다.  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**class**|**tinyint**|참조된 엔터티의 클래스를 식별합니다.<br /><br /> 0 = 개체 또는 열(스키마 바운드가 아닌 참조만 해당)<br /><br /> 1 = 개체 또는 열(스키마 바운드 참조)<br /><br /> 2 = 유형(스키마 바운드 참조)<br /><br /> 3 = XML 스키마 컬렉션(스키마 바운드 참조)<br /><br /> 4 = 파티션 함수(스키마 바운드 참조)|  
|**class_desc**|**nvarchar(60)**|참조된 엔터티의 클래스에 대한 설명입니다.<br /><br /> **OBJECT_OR_COLUMN_REFERENCE_NON_SCHEMA_BOUND**<br /><br /> **OBJECT_OR_COLUMN_REFERENCE_SCHEMA_BOUND**<br /><br /> **TYPE_REFERENCE**<br /><br /> **XML_SCHEMA_COLLECTION_REFERENCE**<br /><br /> **PARTITION_FUNCTION_REFERENCE**|  
|**object_id**|**int**|참조 개체의 ID입니다.|  
|**column_id**|**int**|참조 ID가 열인 경우 참조 열의 ID이며 아닌 경우 0입니다.|  
|**referenced_major_id**|**int**|다음에서 지정한 클래스의 값에 따라 해석되며 참조된 엔터티의 ID입니다.<br /><br /> 0, 1 = 개체 또는 열의 개체 ID<br /><br /> 2 = 유형 ID<br /><br /> 3 = XML 스키마 컬렉션 ID|  
|**referenced_minor_id**|**int**|다음과 같이 클래스의 값에 따라 해석되며 참조된 엔터티의 보조 ID입니다.<br /><br /> 클래스 값과 그에 따른 해석은 다음과 같습니다.<br /><br /> 0, **referenced_minor_id** 는 열 ID는 나이 열이 아닌 경우 0입니다.<br /><br /> 1, **referenced_minor_id** 는 열 ID는 나이 열이 아닌 경우 0입니다.<br /><br /> 그렇지 않으면 **referenced_minor_id** = 0.|  
|**is_selected**|**bit**|개체 또는 열이 선택되었습니다.|  
|**is_updated**|**bit**|개체 또는 열이 업데이트되었습니다.|  
|**is_select_all**|**bit**|개체가 SELECT * 절에서 사용되었습니다(개체 수준만 해당).|  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
