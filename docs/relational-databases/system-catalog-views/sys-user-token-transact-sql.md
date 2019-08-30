---
title: user_token (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.user_token
- user_token
- sys.user_token_TSQL
- user_token_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], security tokens
- sys.user_token catalog view
- user tokens [SQL Server]
- tokens [SQL Server]
- user_token catalog view
ms.assetid: be018103-5e57-43a4-9160-9bf420892aa7
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions|| = azure-sqldw-latest
ms.openlocfilehash: 9b3e389b97cee8a8a6d548eb93ad70b94d09ba40
ms.sourcegitcommit: 71fac5fee00e0eca57e555f44274dd7e08d47e1e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70160744"
---
# <a name="sysuser_token-transact-sql"></a>sys.user_token(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md.md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자 토큰을 구성하는 데이터베이스 보안 주체마다 한 행씩 반환합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**principal_id**|**int**|보안 주체의 ID입니다. 이 값은 데이터베이스 내에서 고유합니다.|  
|**sid**|**varbinary(85)**|보안 주체가 데이터베이스 외부에 정의되어 있는 경우 보안 주체의 보안 식별자입니다. 예를 들어 이 식별자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인, Windows 로그인, Windows 그룹 로그인 또는 인증서에 매핑된 로그인이 될 수 있습니다. 이외의 경우 이 값은 NULL입니다.|  
|**name**|**nvarchar (128)**|보안 주체의 이름입니다. 이 값은 데이터베이스 내에서 고유합니다.|  
|**type**|**nvarchar (128)**|보안 주체 유형에 대한 설명입니다. 모든 유형은 **sid**로 매핑됩니다. 값은 다음 중 하나일 수 있습니다.<br /><br /> SQL USER<br /><br /> WINDOWS LOGIN<br /><br /> WINDOWS GROUP<br /><br /> ROLE<br /><br /> APPLICATION ROLE<br /><br /> DATABASE ROLE<br /><br /> USER MAPPED TO CERTIFICATE<br /><br /> LOGIN MAPPED TO ASYMMETRIC KEY<br /><br /> CERTIFICATE<br /><br /> ASYMMETRIC KEY|  
|**usage**|**nvarchar (128)**|보안 주체가 GRANT 또는 DENY 권한 평가에 참여하도록 지정하거나 인증자의 역할을 하도록 지정합니다.<br /><br /> 이 값은 다음 중 하나일 수 있습니다.<br /><br /> GRANT 또는 DENY<br /><br /> DENY ONLY<br /><br /> AUTHENTICATOR|  
  
## <a name="see-also"></a>관련 항목  
 [login_token &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-login-token-transact-sql.md)   
 [sys.server_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
