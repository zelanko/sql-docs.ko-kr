---
title: sys.trace_events (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- trace_events_TSQL
- trace_events
- sys.trace_events
- sys.trace_events_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trace_events catalog view
ms.assetid: e7d2c5df-0e17-4e94-9d41-d36c7ee60662
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2d564d08dce5dbc89c0071625aefc2cfef80ec36
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37969625"
---
# <a name="systraceevents-transact-sql"></a>sys.trace_events(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **sys.trace_events** 카탈로그 뷰는 모든 SQL 추적 이벤트의 목록을 포함 합니다. 이러한 추적 이벤트는 지정된 버전의 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에 대해 변경되지 않습니다.  
  
> **중요!** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 확장 이벤트 카탈로그 뷰를 사용하십시오.  
  
 이러한 추적 이벤트에 대 한 자세한 내용은 참조 하세요. [SQL Server Event Class Reference](../../relational-databases/event-classes/sql-server-event-class-reference.md)합니다.  
  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**trace_event_id**|**smallint**|이벤트의 고유 ID입니다. 이 열은 또한에 **sys.trace_event_bindings** 하 고 **sys.trace_subclass_values** 카탈로그 뷰.|  
|**category_id**|**smallint**|이벤트의 범주 ID입니다. 이 열은 또한에 **sys.trace_categories** 카탈로그 뷰에 있습니다.|  
|**name**|**nvarchar(128)**|이 이벤트의 고유 이름입니다. 이 매개 변수는 지역화되지 않았습니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고자료  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys.traces &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-traces-transact-sql.md)   
 [sys.trace_categories &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-categories-transact-sql.md)   
 [sys.trace_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-columns-transact-sql.md)   
 [sys.trace_event_bindings &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-event-bindings-transact-sql.md)   
 [sys.trace_subclass_values &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-subclass-values-transact-sql.md)  
  
  
