---
description: sys.trace_events(Transact SQL)
title: sys. trigger_events (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trigger_events_TSQL
- trigger_events
- sys.trigger_events
- sys.trigger_events_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trigger_events catalog view
ms.assetid: 92540447-131c-491c-b033-c064c7d950e1
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ead6f918e85c73d344924bfe1bc7c878bf4d44c6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537987"
---
# <a name="systrigger_events-transact-sql"></a>sys.trace_events(Transact SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  트리거가 실행되는 각 이벤트당 한 개의 행을 포함합니다.  
  
> [!NOTE]  
>  **trigger_events** 이벤트 알림에 적용 되지 않습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<Columns inherited from sys.events>**|해당 없음|는 [sys.debug](../../relational-databases/system-catalog-views/sys-events-transact-sql.md)의 **object_id**, **형식** **type_desc** 열을 상속 합니다.|  
|**is_first**|**bit**|트리거가 해당 이벤트에 대해 처음 실행되도록 표시됩니다.|  
|**is_last**|**bit**|트리거가 해당 이벤트에 대해 마지막에 실행되도록 표시됩니다.|  
|**event_group_type**|**int**|트리거가 생성되는 이벤트 그룹 또는 Null(이벤트 그룹에 생성되지 않은 경우)입니다.|  
|**event_group_type_desc**|**nvarchar(60)**|트리거가 생성되는 이벤트 그룹에 대한 설명 또는 Null(이벤트 그룹에 생성되지 않은 경우)입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
