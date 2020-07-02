---
title: sys. sql_dependencies (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 106c295d200ce823f80988be2276a927aba8126d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85764459"
---
# <a name="syssql_dependencies-transact-sql"></a>sys.sql_dependencies(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] 식에서 참조된 엔터티 또는 다른 개체로의 참조가 정의된 문의 종속성당 한 개의 행을 포함합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]대신 [sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) 를 사용 해야 합니다.  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**class**|**tinyint**|참조된 엔터티의 클래스를 식별합니다.<br /><br /> 0 = 개체 또는 열(스키마 바운드가 아닌 참조만 해당)<br /><br /> 1 = 개체 또는 열(스키마 바운드 참조)<br /><br /> 2 = 유형(스키마 바운드 참조)<br /><br /> 3 = XML 스키마 컬렉션(스키마 바운드 참조)<br /><br /> 4 = 파티션 함수(스키마 바운드 참조)|  
|**class_desc**|**nvarchar(60)**|참조된 엔터티의 클래스에 대한 설명입니다.<br /><br /> **OBJECT_OR_COLUMN_REFERENCE_NON_SCHEMA_BOUND**<br /><br /> **OBJECT_OR_COLUMN_REFERENCE_SCHEMA_BOUND**<br /><br /> **TYPE_REFERENCE**<br /><br /> **XML_SCHEMA_COLLECTION_REFERENCE**<br /><br /> **PARTITION_FUNCTION_REFERENCE**|  
|**object_id**|**int**|참조 개체의 ID입니다.|  
|**column_id**|**int**|참조 ID가 열인 경우 참조 열의 ID이며 아닌 경우 0입니다.|  
|**referenced_major_id**|**int**|다음에서 지정한 클래스의 값에 따라 해석되며 참조된 엔터티의 ID입니다.<br /><br /> 0, 1 = 개체 또는 열의 개체 ID<br /><br /> 2 = 유형 ID<br /><br /> 3 = XML 스키마 컬렉션 ID|  
|**referenced_minor_id**|**int**|다음과 같이 클래스의 값에 따라 해석되며 참조된 엔터티의 보조 ID입니다.<br /><br /> 클래스 값과 그에 따른 해석은 다음과 같습니다.<br /><br /> 0, **referenced_minor_id** 은 열 id입니다. 또는 열이 아닌 경우 0입니다.<br /><br /> 1, **referenced_minor_id** 는 열 id입니다. 또는 열이 아닌 경우 0입니다.<br /><br /> 그렇지 않으면 **referenced_minor_id** = 0입니다.|  
|**is_selected**|**bit**|개체 또는 열이 선택되었습니다.|  
|**is_updated**|**bit**|개체 또는 열이 업데이트되었습니다.|  
|**is_select_all**|**bit**|개체가 SELECT * 절에서 사용되었습니다(개체 수준만 해당).|  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;카탈로그 뷰](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;개체 카탈로그 뷰](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리에 대한 질문과 대답](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
