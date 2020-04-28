---
title: sys. service_queue_usages (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.service_queue_usages
- sys.service_queue_usages_TSQL
- service_queue_usages
- service_queue_usages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_queue_usages catalog view
ms.assetid: d58dcdaf-f82d-43d9-941b-f520581442bf
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8b1cd1c1688922404b882069d9e100504dfbcb14
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68078712"
---
# <a name="sysservice_queue_usages-transact-sql"></a>sys.service_queue_usages(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 카탈로그 뷰는 서비스와 서비스 큐 간의 각 참조에 대해 행을 반환합니다. 서비스는 하나의 큐에만 연결될 수 있으며 큐는 여러 서비스에 연결될 수 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**service_id**|**int**|서비스의 ID입니다. 데이터베이스 내에서 고유합니다. NULL을 허용하지 않습니다.|  
|**service_queue_id**|**int**|서비스에서 사용하는 서비스 큐의 ID입니다. NULL을 허용하지 않습니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [sys.debug &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-services-transact-sql.md)  
  
  
