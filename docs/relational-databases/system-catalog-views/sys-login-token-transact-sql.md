---
title: sys.login_token (Transact SQL) | Microsoft Docs
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
- login_token_TSQL
- sys.login_token_TSQL
- sys.login_token
- login_token
dev_langs:
- TSQL
helpviewer_keywords:
- sys.login_token catalog view
- logins [SQL Server], security tokens
- tokens [SQL Server]
ms.assetid: 86e06938-9d0a-44e5-99e2-55c8ef5f2f84
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 8ffa2027c83f8aebfb64a936b70cbee527526a51
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33180689"
---
# <a name="syslogintoken-transact-sql"></a>sys.login_token(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  로그인 토큰의 일부인 모든 각 서버 보안 주체당 한 개의 행을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**principal_id**|**int**|보안 주체의 ID입니다. 이 값은 서버 내에서 고유합니다.|  
|**sid**|**varbinary(85)**|보안 주체의 SID(보안 ID)입니다. Windows 보안 주체, 이것이 **sid** = Windows SID입니다. 로그인, 인증서에 매핑된 경우 **sid** 인증서에서 GUID = 합니다.|  
|**name**|**nvarchar(128)**|보안 주체의 이름입니다. 이 값은 서버 내에서 고유합니다.|  
|**type**|**nvarchar(128)**|보안 주체 유형에 대한 설명입니다. 모든 형식에 매핑됩니다. **sid**합니다. 이 값은<br /><br /> SQL LOGIN<br /><br /> WINDOWS LOGIN<br /><br /> WINDOWS GROUP<br /><br /> SERVER ROLE<br /><br /> LOGIN MAPPED TO CERTIFICATE<br /><br /> LOGIN MAPPED TO ASYMMETRIC KEY<br /><br /> CERTIFICATE<br /><br /> ASYMMETRIC KEY|  
|**사용**|**nvarchar(128)**|보안 주체가 GRANT 또는 DENY 권한 평가에 참여하도록 지정하거나 인증자의 역할을 하도록 지정합니다.<br /><br /> 이 값은 다음 중 하나일 수 있습니다.<br /><br /> GRANT 또는 DENY<br /><br /> DENY ONLY<br /><br /> AUTHENTICATOR|  
  
## <a name="see-also"></a>관련 항목:  
 [sys.user_token &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-user-token-transact-sql.md)   
 [sys.server_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
