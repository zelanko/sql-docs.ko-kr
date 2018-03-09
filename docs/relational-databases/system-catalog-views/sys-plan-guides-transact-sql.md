---
title: sys.plan_guides (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.planguides_TSQL
- plan_guides
- sys.planguides
- plan_guides_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.plan_guides catalog view
ms.assetid: 3dde0397-ef6f-4b3f-8250-3f25584eb62b
caps.latest.revision: "24"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 591bc781d6c156320dffcb06e6e541aeb5b669a3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sysplanguides-transact-sql"></a>sys.plan_guides(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  데이터베이스 내의 각 계획 지침당 한 개의 행을 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**plan_guide_id**|**int**|데이터베이스의 계획 지침 고유 식별자입니다.|  
|**name**|**sysname**|계획 지침의 이름입니다.|  
|**create_date**|**datetime**|계획 지침을 만든 날짜와 시간입니다.|  
|**modify_date**|**날짜/시간**|계획 지침을 마지막으로 수정한 날짜입니다.|  
|**is_disabled**|**bit**|1 = 계획 지침이 비활성화되어 있습니다.<br /><br /> 0 = 계획 지침이 활성화되어 있습니다.|  
|**query_text**|**nvarchar(max)**|계획 지침이 생성된 쿼리의 텍스트입니다.|  
|**scope_type**|**tinyint**|계획 지침 범위를 식별합니다.<br /><br /> 1 = OBJECT<br /><br /> 2 = SQL<br /><br /> 3 = TEMPLATE|  
|**scope_type_desc**|**nvarchar (60)**|계획 지침의 범위에 대한 설명입니다.<br /><br /> OBJECT<br /><br /> SQL<br /><br /> TEMPLATE|  
|**scope_object_id**|**Int**|범위가 OBJECT인 경우 계획 지침의 범위를 정의하는 개체의 object_id입니다.<br /><br /> 계획 지침 범위가 OBJECT가 아니면 NULL입니다.|  
|**scope_batch**|**nvarchar(max)**|경우 일괄 처리 텍스트 **scope_type** 은 SQL입니다.<br /><br /> 일괄 처리 형식이 SQL이 아니면 NULL입니다.<br /><br /> Null 인 경우 및 **scope_type** sql 일의 값 **query_text** 적용 됩니다.|  
|**매개 변수**|**nvarchar(max)**|계획 지침과 연결된 매개 변수 목록을 정의하는 문자열입니다.<br /><br /> NULL = 계획 지침에 연결되는 매개 변수 목록이 없습니다.|  
|**힌트**|**nvarchar(max)**|계획 지침과 연결된 OPTION 절 힌트입니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sp_create_plan_guide&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
  
