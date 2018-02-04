---
title: sys.trace_event_bindings (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
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
- sys.trace_event_bindings_TSQL
- trace_event_bindings
- sys.trace_event_bindings
- trace_event_bindings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trace_event_bindings catalog view
ms.assetid: 22f534e1-4ed6-4b3e-9ead-1d1001a1b0f5
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 276ce6340b72d7c945f55ea9ea27a3a28caba158
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="systraceeventbindings-transact-sql"></a>sys.trace_event_bindings(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **sys.trace_event_bindings** 카탈로그 뷰에 가능한 모든 사용 조합 이벤트 및 열 목록이 포함 되어 있습니다. 에 나열 된 각 이벤트에 대 한는 **trace_event_id** 열에서 사용 가능한 모든 열에 나열 되는 **trace_column_id** 열입니다. 지정된 이벤트가 발생할 때마다 사용 가능한 모든 열이 채워지는 것은 아닙니다. 지정된 버전의 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서는 이러한 값이 변경되지 않습니다.  
  
 지원 되는 추적 이벤트의 전체 목록은 참조 하십시오. [SQL Server Event Class Reference](../../relational-databases/event-classes/sql-server-event-class-reference.md)합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 확장 이벤트 카탈로그 뷰를 대신 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**trace_event_id**|**smallint**|추적 이벤트의 ID입니다. 이 열은 또한에 **sys.trace_events** 카탈로그 뷰에 있습니다.|  
|**trace_column_id**|**smallint**|추적 열의 ID입니다. 이 열은 또한에 **sys.trace_columns** 카탈로그 뷰에 있습니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [개체 카탈로그 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys.traces &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-traces-transact-sql.md)   
 [sys.trace_categories &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-trace-categories-transact-sql.md)   
 [sys.trace_columns &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-trace-columns-transact-sql.md)   
 [sys.trace_events &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-trace-events-transact-sql.md)   
 [sys.trace_subclass_values &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-trace-subclass-values-transact-sql.md)  
  
  
