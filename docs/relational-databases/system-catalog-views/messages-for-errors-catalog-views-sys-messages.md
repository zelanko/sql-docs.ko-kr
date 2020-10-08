---
description: 오류 메시지 카탈로그 뷰 - sys.messages
title: sys. messages (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 30cfb208d709f19743216369b23e6b7bef9dfc38
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810399"
---
# <a name="messages-for-errors-catalog-views---sysmessages"></a>오류 메시지 카탈로그 뷰 - sys.messages
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  시스템 정의 및 사용자 정의 메시지 모두에 대해 시스템의 오류 메시지에 대 한 각 **message_id** 또는 **language_id** 에 대 한 행을 포함 합니다. 자세한 내용은 [sp_addmessage&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)을 참조하세요.  
   
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**message_id**|**int**|메시지의 ID입니다. 서버 전체에서 고유하며 50000 미만의 메시지 ID가 시스템 메시지입니다.|  
|**language_id**|**smallint**|**Sys.syslanguages**에 정의 된 **텍스트** 텍스트가 사용 되는 언어 ID입니다. 이는 지정 된 **message_id**에 대해 고유 합니다.|  
|**severity**|**tinyint**|1에서 25 사이의 메시지 심각도입니다. 이는 **message_id**내의 모든 메시지 언어에 대해 동일 합니다.|  
|**is_event_logged**|**bit**|1 = 오류가 발생하면 메시지가 이벤트 로깅됩니다. 이는 **message_id**내의 모든 메시지 언어에 대해 동일 합니다.|  
|**text**|**nvarchar(2048)**|해당 **language_id** 활성 상태일 때 사용 되는 메시지 텍스트입니다.|  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;&#41; 카탈로그 뷰의 오류에 대 한 메시지 &#40;]()   
 [예외 메시지 상자 프로그래밍](/previous-versions/sql/sql-server-2016/ms166343(v=sql.130))   
 [오류 메시지](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [데이터베이스 엔진 이벤트 및 오류](../../relational-databases/errors-events/database-engine-events-and-errors.md)  
  
