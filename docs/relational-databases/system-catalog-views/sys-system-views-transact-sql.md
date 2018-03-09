---
title: sys.system_views (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.system_views_TSQL
- system_views
- system_views_TSQL
- sys.system_views
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_views catalog view
ms.assetid: a526c410-e7b5-4075-8103-e1f3c6837c3c
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5db3ad63df2d57856ffd9d89122290999f69a860
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="syssystemviews-transact-sql"></a>sys.system_views(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에 포함된 각 시스템 뷰당 한 개의 행을 포함합니다. 스키마에 포함 된 모든 시스템 뷰 **sys** 또는 **INFORMATION_SCHEMA**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|\<열을 상속 >||이 뷰가 상속 하는 열 목록은 참조 [sys.objects&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**is_replicated**|**bit**|1 = 뷰가 복제됩니다.|  
|**has_replication_filter**|**bit**|1 = 뷰에 복제 필터가 있습니다.|  
|**has_opaque_metadata**|**bit**|1 = 뷰에 VIEW_METADATA 옵션이 지정되었습니다. 자세한 내용은 [CREATE VIEW&#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)를 참조하세요.|  
|**has_unchecked_assembly_data**|**bit**|1 = 테이블은 마지막 ALTER ASSEMBLY를 수행하는 동안 정의가 변경된 어셈블리에 종속되어 있는 데이터를 포함합니다. 다음 번 DBCC CHECKDB 또는 DBCC CHECKTABLE이 성공적으로 수행된 후에 다시 0으로 설정됩니다.|  
|**with_check_option**|**bit**|1 = 뷰 정의에 WITH CHECK OPTION이 지정되었습니다.|  
|**is_date_correlation_view**|**bit**|1 = 뷰가 시스템 간에 상관 관계 정보를 저장 하는 데 자동으로 만들어진 **datetime** 열입니다. DATE_CORRELATION_OPTIMIZATION을 ON으로 설정하여 이 뷰를 생성하도록 설정했습니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [개체 카탈로그 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [DBCC CHECKDB&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)   
 [DBCC CHECKTABLE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)   
 [ALTER ASSEMBLY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
  
