---
description: sys.event_notifications(Transact-SQL)
title: sys. event_notifications (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 100faecd43b0a76bea9aa11aa8bdff3055aa7f5f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486392"
---
# <a name="sysevent_notifications-transact-sql"></a>sys.event_notifications(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  이벤트 알림과 함께 각 개체에 대해 행을 반환 **합니다. 여기서는 sys. type** = EN입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|이벤트 알림 이름입니다.|  
|**object_id**|**int**|개체 ID입니다. 데이터베이스 내에서 고유합니다.|  
|**parent_class**|**tinyint**|부모 클래스입니다.<br /><br /> 0 = 데이터베이스<br /><br /> 1 = 개체 또는 열|  
|**parent_class_desc**|**nvarchar(60)**|DATABASE<br /><br /> OBJECT_OR_COLUMN|  
|**parent_id**|**int**|부모 개체의 0이 아닌 ID입니다.<br /><br /> 0 = 부모 클래스는 데이터베이스입니다.|  
|**create_date**|**datetime**|만든 날짜입니다.|  
|**modify_date**|**datetime**|항상 **create_date**와 같습니다.|  
|**service_name**|**nvarchar(256)**|알림을 보낸 대상 서비스의 이름입니다.|  
|**broker_instance**|**nvarchar(128)**|알림을 보낸 Broker 인스턴스입니다.|  
|**principal_id**|**int**|이 이벤트 알림을 소유한 데이터베이스 보안 주체의 ID입니다.|  
|**creator_sid**|**varbinary(85)**|이벤트 알림을 만든 로그인의 SID입니다.<br /><br /> FAN_IN 옵션이 지정되어 있지 않으면 NULL입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
