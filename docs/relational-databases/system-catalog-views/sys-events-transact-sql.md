---
title: sys. events (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.events_TSQL
- sys.events
- events_TSQL
- events
dev_langs:
- TSQL
helpviewer_keywords:
- sys.events catalog view
ms.assetid: f245a97a-80fc-43fb-a6e4-139420c9a47a
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2c6c0fcffae318e13025d63c7a244f44de8689f4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85724675"
---
# <a name="sysevents-transact-sql"></a>sys.events(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  트리거 또는 이벤트 알림이 실행되는 각 이벤트마다 행이 하나 있습니다. 이러한 이벤트는 [CREATE trigger](../../t-sql/statements/create-trigger-transact-sql.md) 또는 [create event notification](../../t-sql/statements/create-event-notification-transact-sql.md)을 사용 하 여 트리거 또는 이벤트 알림을 만들 때 지정 되는 이벤트 유형을 나타냅니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|트리거 또는 이벤트 알림의 ID입니다. 이 값은 **형식과**함께 행을 고유 하 게 식별 합니다.|  
|**type**|**int**|트리거를 발생시키는 이벤트입니다.|  
|**type_desc**|**nvarchar(60)**|트리거를 실행시키는 이벤트에 대한 설명입니다.|  
|**is_trigger_event**|**bit**|1 = 트리거 이벤트<br /><br /> 0 = 알림 이벤트|  
|**event_group_type**|**int**|트리거나 이벤트 알림이 생성되는 이벤트 그룹 또는 Null(이벤트 그룹에 생성되지 않은 경우)입니다.|  
|**event_group_type_desc**|**nvarchar(60)**|트리거나 이벤트 알림이 생성되는 이벤트 그룹에 대한 설명 또는 Null(이벤트 그룹에 생성되지 않은 경우)입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;개체 카탈로그 뷰](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
