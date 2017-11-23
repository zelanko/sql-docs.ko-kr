---
title: sys.procedures (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- procedures
- sys.procedures_TSQL
- sys.procedures
- procedures_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.procedures catalog view
ms.assetid: d17af274-b2dd-464e-9523-ee1f43e1455b
caps.latest.revision: "20"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 62640bc781b5c6be11fed4129a2b467e7b74c93c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sysprocedures-transact-sql"></a>sys.procedures(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  각 개체와는 어떤 종류의 프로시저에 대 한 행을 포함 **sys.objects.type** = P, X, RF 및 PC입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<Sys.objects에서 상속 된 열 >**||이 뷰가 상속 하는 열 목록은 참조 [sys.objects&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)|  
|**is_auto_executed**|**bit**|1인 경우 서버 시작 시 프로시저가 자동으로 실행됩니다. 자동으로 실행하지 않으려면 0으로 설정합니다. master 데이터베이스의 프로시저에 대해서만 설정할 수 있습니다.|  
|**is_execution_replicated**|**bit**|이 프로시저의 실행이 복제됩니다.|  
|**is_repl_serializable_only**|**bit**|프로시저 실행 복제는 트랜잭션을 직렬화할 수 있는 경우에만 수행됩니다.|  
|**skips_repl_constraints**|**bit**|실행하는 동안 프로시저는 NOT FOR REPLICATION이라고 표시된 제약 조건을 건너뜁니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [개체 카탈로그 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
