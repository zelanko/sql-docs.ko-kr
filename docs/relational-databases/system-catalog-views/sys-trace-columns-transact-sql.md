---
title: sys. trace_columns (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.trace_columns
- trace_columns
- trace_columns_TSQL
- sys.trace_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trace_columns catalog view
ms.assetid: 5c48eb09-9e9b-45dd-b151-ca39b026ece5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8dc7177f58819720e9778f3bf363c98d6e15a295
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896451"
---
# <a name="systrace_columns-transact-sql"></a>sys.trace_columns(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Trace_columns** 카탈로그 뷰는 모든 추적 이벤트 열 목록을 포함 합니다. 지정된 버전의 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서는 이러한 열이 변경되지 않습니다.  
  
 지원 되는 추적 이벤트의 전체 목록은 [SQL Server 이벤트 클래스 참조](../../relational-databases/event-classes/sql-server-event-class-reference.md)를 참조 하세요.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 확장 이벤트 카탈로그 뷰를 사용하십시오.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**trace_column_id**|**smallint**|이 열의 고유 ID입니다.|  
|**name**|**nvarchar(128)**|이 열의 고유 이름입니다. 이 매개 변수는 지역화되지 않았습니다.|  
|**type_name**|**nvarchar(128)**|이 열의 데이터 형식 이름입니다.|  
|**max_size**|**int**|이 열의 최대 데이터 크기(바이트)입니다.|  
|**is_filterable**|**bit**|필터 사양에서 열을 사용할 수 있는지 여부를 나타냅니다.<br /><br /> 0 = false<br /><br /> 1 = true|  
|**is_repeatable**|**bit**|"반복되는 열" 데이터에서 열을 참조할 수 있는지 여부를 나타냅니다.<br /><br /> 0 = false<br /><br /> 1 = true|  
|**is_repeated_base**|**bit**|참조하는 반복되는 데이터의 고유 키로 이 열이 사용되는지 여부를 나타냅니다.<br /><br /> 0 = false<br /><br /> 1 = true|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;개체 카탈로그 뷰](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys.debug &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-traces-transact-sql.md)   
 [trace_categories &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-categories-transact-sql.md)   
 [trace_events &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-events-transact-sql.md)   
 [trace_event_bindings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-event-bindings-transact-sql.md)   
 [trace_subclass_values &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-subclass-values-transact-sql.md)  
  
  
