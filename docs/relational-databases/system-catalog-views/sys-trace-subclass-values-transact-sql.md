---
description: sys.trace_subclass_values(Transact-SQL)
title: sys. trace_subclass_values (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.trace_subclass_values
- trace_subclass_values_TSQL
- sys.trace_subclass_values_TSQL
- trace_subclass_values
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trace_subclass_values catalog view
ms.assetid: 542b19ca-61c8-41ca-aa2e-0aba8906cc24
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 17d3b47e0e151aca5603ec8ea01e2d5e0a0aec02
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542431"
---
# <a name="systrace_subclass_values-transact-sql"></a>sys.trace_subclass_values(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Sys. trace_subclass_values** 카탈로그 뷰에는 명명 된 열 값 목록이 포함 되어 있습니다. 지정된 버전의 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서는 이러한 하위 클래스 값이 변경되지 않습니다.  
  
 지원 되는 추적 이벤트의 전체 목록은 [SQL Server 이벤트 클래스 참조](../../relational-databases/event-classes/sql-server-event-class-reference.md)를 참조 하세요.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 확장 이벤트 카탈로그 뷰를 사용하십시오.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**trace_event_id**|**smallint**|추적 이벤트의 ID입니다. 이 매개 변수는 또한 **sys. trace_events** 카탈로그 뷰에 있습니다.|  
|**trace_column_id**|**smallint**|열거에 사용된 추적 열의 ID입니다. 이 매개 변수는 또한 **sys. trace_columns** 카탈로그 뷰에 있습니다.|  
|**subclass_name**|**nvarchar(128)**|열 값의 의미입니다.|  
|**subclass_value**|**smallint**|열 값입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys.debug &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-traces-transact-sql.md)   
 [trace_categories &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-categories-transact-sql.md)   
 [trace_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-columns-transact-sql.md)   
 [trace_events &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-events-transact-sql.md)   
 [trace_event_bindings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-event-bindings-transact-sql.md)  
  
  
