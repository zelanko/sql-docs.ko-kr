---
title: ALTER REMOTE SERVICE BINDING(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER REMOTE SERVICE BINDING
- ALTER_REMOTE_SERVICE_BINDING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- remote service bindings [Service Broker], modifying
- ALTER REMOTE SERVICE BINDING statement
- modifying remote service bindings
ms.assetid: ee620b4a-9375-4eaa-a016-69916c9e1e68
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 5985acaca76b19a1a863ecc066f6a9da9b900008
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33066050"
---
# <a name="alter-remote-service-binding-transact-sql"></a>ALTER REMOTE SERVICE BINDING(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  원격 서비스 바인딩에 연결된 사용자를 변경하거나 바인딩에 대한 익명 인증 설정을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
ALTER REMOTE SERVICE BINDING binding_name   
   WITH [ USER = <user_name> ] [ , ANONYMOUS = { ON | OFF } ]   
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *binding_name*  
 변경할 원격 서비스 바인딩의 이름입니다. 서버, 데이터베이스 및 스키마 이름은 지정될 수 없습니다.  
  
 WITH USER = \<*user_name>*  
 이 바인딩에 대한 원격 서비스에 연결된 인증서를 보유하고 있는 데이터베이스 사용자를 지정합니다. 이 인증서의 공개 키는 원격 서비스와 교환하는 메시지를 암호화하고 인증하는 데 사용됩니다.  
  
 ANONYMOUS  
 원격 서비스와 통신할 경우 익명 인증을 사용할지 여부를 지정합니다. ANONYMOUS = ON인 경우 익명 인증이 사용되며 로컬 사용자의 자격 증명이 원격 서비스로 전송되지 않습니다. ANONYMOUS = OFF인 경우 사용자 자격 증명이 전송됩니다. 이 절을 지정하지 않은 경우 기본값은 OFF입니다.  
  
## <a name="remarks"></a>Remarks  
 *user_name*과 연관된 인증서에 있는 공개 키는 원격 서비스로 전달된 메시지 인증 및 대화를 암호화하는 데 사용되는 세션 키의 암호화에 사용됩니다. *user_name*에 대한 인증서는 원격 서비스를 호스팅하는 데이터베이스 로그인에 대한 인증서와 일치해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 원격 서비스 바인딩을 변경할 수 있는 권한은 기본적으로 원격 서비스 바인딩의 소유자, **db_owner** 고정 데이터베이스 역할의 멤버 및 **sysadmin** 고정 서버 역할의 멤버로 설정됩니다.  
  
 ALTER REMOTE SERVICE BINDING 문을 실행하는 사용자에게는 이 문에 지정된 사용자를 가장할 수 있는 권한이 있어야 합니다.  
  
 원격 서비스 바인딩에 대한 AUTHORIZATION을 변경하려면 ALTER AUTHORIZATION 문을 사용합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `APBinding` 계정의 인증서를 사용하여 메시지를 암호화하도록 원격 서비스 바인딩 `SecurityAccount`을 변경합니다.  
  
```  
ALTER REMOTE SERVICE BINDING APBinding  
    WITH USER = SecurityAccount ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE REMOTE SERVICE BINDING&#40;Transact-SQL&#41;](../../t-sql/statements/create-remote-service-binding-transact-sql.md)   
 [DROP REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/drop-remote-service-binding-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
