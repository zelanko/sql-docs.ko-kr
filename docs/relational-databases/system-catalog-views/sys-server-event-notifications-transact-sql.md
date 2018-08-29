---
title: sys.server_event_notifications (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- server_event_notifications
- sys.server_event_notifications
- sys.server_event_notifications_TSQL
- server_event_notifications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_notifications catalog view
ms.assetid: 1a83a044-3130-4551-95ca-162525846ff5
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 91e033b5931f00761cb79e208287c784cf3ecd5e
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43026531"
---
# <a name="sysservereventnotifications-transact-sql"></a>sys.server_event_notifications(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서버 수준의 각 이벤트 알림 개체당 하나의 행을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|서버 이벤트 알림의 이름이며 전체 서버 수준 이벤트 알림에 걸쳐 고유합니다.|  
|**object_id**|**int**|개체 ID입니다. 내에서 고유 합니다 **마스터** 데이터베이스입니다.|  
|**parent_class**|**tinyint**|부모 클래스입니다. 항상 100 = Server입니다.|  
|**parent_class_desc**|**nvarchar(60)**|부모 클래스에 대한 설명입니다. 항상 SERVER입니다.|  
|**parent_id**|**int**|항상 0입니다.|  
|**create_date**|**datetime**|만든 날짜입니다.|  
|**modify_date**|**datetime**|ALTER 문을 사용하여 개체를 마지막으로 수정한 날짜입니다.|  
|**service_name**|**nvarchar(256)**|알림을 보낸 대상 서비스의 이름입니다.|  
|**broker_instance**|**nvarchar(128)**|명명된 대상 서비스가 정의되는 Service Broker입니다.|  
|**creator_sid**|**varbinary(85)**|이벤트 알림을 만드는 문을 실행하는 로그인의 SID입니다. 이벤트 알림 정의에서 WITH FAN_IN을 지정하지 않으면 NULL이 됩니다.|  
|**principal_id**|**int**|이를 소유하는 서버 보안 주체의 ID입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
