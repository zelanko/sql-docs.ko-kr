---
title: sys. trace_categories (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trace_categories
- trace_categories_TSQL
- sys.trace_categories
- sys.trace_categories_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trace_categories catalog view
ms.assetid: f6a86766-e2a9-4d9f-a073-1b59e888ba7d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c9685b9733c1d13b79ef2a19ee2f19bbe3130426
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68106669"
---
# <a name="systrace_categories-transact-sql"></a>sys.trace_categories(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  유사한 이벤트 클래스는 범주별로 그룹화됩니다. **Trace_categories** 카탈로그 뷰의 각 행은 서버에서 고유한 범주를 식별 합니다. 이 범주는 지정된 버전의 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에 대해 변경되지 않습니다.  
  
 지원 되는 추적 이벤트의 전체 목록은 [SQL Server 이벤트 클래스 참조](../../relational-databases/event-classes/sql-server-event-class-reference.md)를 참조 하세요.  
  
> **중요 한!** 
  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 확장 이벤트 카탈로그 뷰를 사용하십시오.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**category_id**|**smallint**|이 범주의 고유 ID입니다. 이 열은 **sys. trace_events** 카탈로그 뷰에도 있습니다.|  
|**name**|**nvarchar(128)**|이 범주의 고유 이름입니다. 이 매개 변수는 지역화되지 않았습니다.|  
|**type**|**tinyint**|범주 유형:<br /><br /> 0 = 보통<br /><br /> 1 = 연결<br /><br /> 2 = 오류|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;개체 카탈로그 뷰](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys.debug &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-traces-transact-sql.md)   
 [trace_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-columns-transact-sql.md)   
 [trace_events &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-events-transact-sql.md)   
 [trace_event_bindings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-event-bindings-transact-sql.md)   
 [trace_subclass_values &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-trace-subclass-values-transact-sql.md)  
  
  
