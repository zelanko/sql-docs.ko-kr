---
title: sys.messages (Transact SQL) | Microsoft Docs
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
- messages_TSQL
- sys.messages_TSQL
- sys.messages
- messages
dev_langs:
- TSQL
helpviewer_keywords:
- error messages [SQL Server]
- sys.messages catalog view
- error numbers [SQL Server]
ms.assetid: 8c16ecdf-68f4-4a2a-b594-086e3344e58a
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 07a5a426c0a2cf0b4b7c0385850471c3580d4fd3
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33178999"
---
# <a name="messages-for-errors-catalog-views---sysmessages"></a>오류 메시지 카탈로그 뷰-sys.messages
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  각각에 대해 한 행을 포함 **message_id** 또는 **language_id** 모두 시스템 정의 및 사용자 정의 메시지에 대 한 시스템의 오류 메시지입니다. 자세한 내용은 [sp_addmessage&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)을 참조하세요.  
   
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**message_id**|**int**|메시지의 ID입니다. 서버 전체에서 고유하며 50000 미만의 메시지 ID가 시스템 메시지입니다.|  
|**language_id**|**smallint**|언어 ID입니다의 텍스트 **텍스트** 에 정의 된 대로 사용 됩니다 **syslanguages**합니다. 지정 된 항목에 대 한 고유 **message_id**합니다.|  
|**severity**|**tinyint**|1에서 25 사이의 메시지 심각도입니다. 이것은 동일한 내의 모든 메시지 언어는 **message_id**합니다.|  
|**is_event_logged**|**bit**|1 = 오류가 발생하면 메시지가 이벤트 로깅됩니다. 이것은 동일한 내의 모든 메시지 언어는 **message_id**합니다.|  
|**text**|**nvarchar(2048)**|메시지의 텍스트를 사용 하는 경우 해당 **language_id** 활성화 되어 있습니다.|  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [메시지 &#40;오류에 대 한&#41; 카탈로그 뷰 &#40;Transact SQL&#41;](http://msdn.microsoft.com/library/8ac78c53-7b97-41b3-9cbd-5f97c179f1f2)   
 [예외 메시지 상자 프로그래밍](http://msdn.microsoft.com/library/0b1ba514-6959-4e69-bfd2-3cf3c1ac4b9c)   
 [오류 메시지](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [데이터베이스 엔진 이벤트 및 오류](../../relational-databases/errors-events/database-engine-events-and-errors.md)  
  
  
