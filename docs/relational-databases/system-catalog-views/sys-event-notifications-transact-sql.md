---
title: sys.event_notifications (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- event_notifications_TSQL
- event_notifications
- sys.event_notifications_TSQL
- sys.event_notifications
dev_langs:
- TSQL
helpviewer_keywords:
- sys.event_notifications catalog view
ms.assetid: 136a76ee-2b35-4418-ab46-fda2d51f7d99
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 1b07ca793821b39a549e709f52fa57bf1dd32dcb
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39562097"
---
# <a name="syseventnotifications-transact-sql"></a>sys.event_notifications(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  이벤트 알림이 된 각 개체에 대 한 행을 반환 **sys.objects.type** = EN입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|이벤트 알림 이름입니다.|  
|**object_id**|**int**|개체 ID입니다. 데이터베이스 내에서 고유합니다.|  
|**parent_class**|**tinyint**|부모 클래스입니다.<br /><br /> 0 = 데이터베이스<br /><br /> 1 = 개체 또는 열|  
|**parent_class_desc**|**nvarchar(60)**|DATABASE<br /><br /> OBJECT_OR_COLUMN|  
|**parent_id**|**int**|부모 개체의 0이 아닌 ID입니다.<br /><br /> 0 = 부모 클래스는 데이터베이스입니다.|  
|**create_date**|**datetime**|만든 날짜입니다.|  
|**modify_date**|**datetime**|항상 **create_date**합니다.|  
|**service_name**|**nvarchar(256)**|알림을 보낸 대상 서비스의 이름입니다.|  
|**broker_instance**|**nvarchar(128)**|알림을 보낸 Broker 인스턴스입니다.|  
|**principal_id**|**int**|이 이벤트 알림을 소유한 데이터베이스 보안 주체의 ID입니다.|  
|**creator_sid**|**varbinary(85)**|이벤트 알림을 만든 로그인의 SID입니다.<br /><br /> FAN_IN 옵션이 지정되어 있지 않으면 NULL입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
