---
title: CREATE REMOTE SERVICE BINDING(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE REMOTE SERVICE BINDING
- SERVICE_BINDING_TSQL
- CREATE REMOTE SERVICE
- REMOTE_TSQL
- CREATE_REMOTE_SERVICE_BINDING_TSQL
- CREATE_REMOTE_SERVICE_TSQL
- BINDING
- SERVICE BINDING
- BINDING_TSQL
- CREATE_REMOTE_TSQL
- REMOTE_SERVICE_TSQL
- CREATE REMOTE
- REMOTE SERVICE
- REMOTE_SERVICE_BINDING_TSQL
- REMOTE
- REMOTE SERVICE BINDING
dev_langs:
- TSQL
helpviewer_keywords:
- binding remote service [Service Broker]
- dialog security [Service Broker]
- end-to-end security [Service Broker]
- security [Service Broker], remote service bindings
- CREATE REMOTE SERVICE BINDING statement
- conversation security [Service Broker]
- remote service bindings [Service Broker], creating
ms.assetid: 4165c404-4d50-4063-9a6e-6e267d309376
caps.latest.revision: 46
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a1313143e96658fd2d7b19193726af371fce70f1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="create-remote-service-binding-transact-sql"></a>CREATE REMOTE SERVICE BINDING(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  원격 서비스와 대화를 시작하는 데 사용할 보안 자격 증명을 정의하는 바인딩을 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE REMOTE SERVICE BINDING binding_name   
   [ AUTHORIZATION owner_name ]   
   TO SERVICE 'service_name'   
   WITH  USER = user_name [ , ANONYMOUS = { ON | OFF } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *binding_name*  
 생성할 원격 서비스 바인딩의 이름입니다. 서버, 데이터베이스 및 스키마 이름은 지정될 수 없습니다. *binding_name*은 유효한 **sysname**이어야 합니다.  
  
 AUTHORIZATION *owner_name*  
 지정한 데이터베이스 사용자 또는 역할로 바인딩 소유자를 설정합니다. 현재 사용자가 **dbo** 또는 **sa**일 경우 *owner_name*은 유효한 사용자 또는 역할의 이름일 수 있습니다. 그렇지 않으면 *owner_name*은 현재 사용자 이름, 현재 사용자에 IMPERSONATE 권한이 있는 사용자 이름 또는 현재 사용자가 속해 있는 역할 이름 중 하나여야 합니다.  
  
 TO SERVICE '*service_name*'  
 WITH USER 절에서 식별된 사용자에 바인딩할 원격 서비스를 지정합니다.  
  
 USER = *user_name*  
 TO SERVICE 절로 식별되는 원격 서비스와 연결된 인증서를 소유하는 데이터베이스 보안 주체를 지정합니다. 이 인증서는 원격 서비스와 교환한 메시지의 암호화 및 인증에 사용됩니다.  
  
 ANONYMOUS  
 원격 서비스와 통신할 경우 익명 인증을 사용할지 여부를 지정합니다. ANONYMOUS가 ON인 경우에는 익명 인증이 사용되고 원격 데이터베이스의 작업은 **public** 고정 데이터베이스 역할의 멤버로 수행됩니다. ANONYMOUS가 OFF인 경우에는 원격 데이터베이스의 작업이 해당 데이터베이스의 특정 사용자로 수행됩니다. 이 절을 지정하지 않은 경우 기본값은 OFF입니다.  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 원격 서비스 바인딩을 사용하여 새 대화에 사용할 인증서를 찾습니다. *user_name*과 연관된 인증서에 있는 공개 키는 원격 서비스로 전달된 메시지 인증 및 대화를 암호화하는 데 사용되는 세션 키의 암호화에 사용됩니다. *user_name*에 대한 인증서는 원격 서비스를 호스팅하는 데이터베이스의 사용자에 대한 인증서와 일치해야 합니다.  
  
 원격 서비스 바인딩은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 외부의 대상 서비스와 대화하는 시작 서비스에만 필요합니다. 시작 서비스를 호스팅하는 데이터베이스에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 외부의 대상 서비스에 대한 원격 서비스 바인딩이 포함되어야 합니다. 대상 서비스를 호스팅하는 데이터베이스에는 대상 서비스와 대화하는 시작 서비스에 대한 원격 서비스 바인딩이 없어도 됩니다. 시작자와 대상 서비스가 동일한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내에 있는 경우에는 원격 서비스 바인딩이 필요 없습니다. 그러나 원격 서비스 바인딩이 있고 TO SERVICE에 지정된 *service_name*이 로컬 서비스 이름과 일치하면 [!INCLUDE[ssSB](../../includes/sssb-md.md)]이 해당 바인딩을 사용하게 됩니다.  
  
 ANONYMOUS가 ON인 경우 시작 서비스는 **public** 고정 데이터베이스 역할의 멤버로 대상 서비스에 연결합니다. 기본적으로 이 역할의 멤버는 데이터베이스에 연결할 수 있는 권한이 없습니다. 메시지를 보내려면 대상 데이터베이스가 데이터베이스에 대한 CONNECT 권한 및 대상 서비스에 대한 SEND 권한을 **public** 역할에 부여해야 합니다.  
  
 사용자가 인증서를 두 개 이상 소유하고 있는 경우 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 현재 유효하며 AVAILABLE FOR BEGIN_DIALOG로 표시된 인증서 중에서 만료 날짜가 가장 최근인 인증서를 선택합니다.  
  
## <a name="permissions"></a>사용 권한  
 원격 서비스 바인딩 생성 권한은 기본적으로 USER 절에 명명된 사용자, **db_owner** 고정 데이터베이스 역할의 멤버, **db_ddladmin** 고정 데이터베이스 역할의 멤버 및 **sysadmin** 고정 서버 역할의 멤버에게 있습니다.  
  
 CREATE REMOTE SERVICE BINDING 문을 실행하는 사용자는 문에서 지정한 보안 주체에 대해 가장 권한이 있어야 합니다.  
  
 원격 서비스 바인딩은 임시 개체가 될 수 없습니다. 원격 서비스 바인딩 이름은 **#** 으로 시작할 수 있지만 영구 개체입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-remote-service-binding"></a>1. 원격 서비스 바인딩 만들기  
 다음 예에서는 `//Adventure-Works.com/services/AccountsPayable` 서비스에 대한 바인딩을 만듭니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 `APUser` 데이터베이스 보안 주체가 소유한 인증서를 사용하여 해당 원격 서비스와 세션 암호화 키를 교환합니다.  
  
```  
CREATE REMOTE SERVICE BINDING APBinding  
    TO SERVICE '//Adventure-Works.com/services/AccountsPayable'  
    WITH USER = APUser ;  
```  
  
### <a name="b-creating-a-remote-service-binding-using-anonymous-authentication"></a>2. 익명 인증을 사용하여 원격 서비스 바인딩 만들기  
 다음 예에서는 `//Adventure-Works.com/services/AccountsPayable` 서비스에 대한 바인딩을 만듭니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 `APUser` 데이터베이스 보안 주체가 소유한 인증서를 사용하여 해당 원격 서비스와 세션 암호화 키를 교환합니다. 원격 서비스를 인증하지는 않습니다. 원격 서비스를 호스팅하는 데이터베이스에서 메시지는 **guest** 사용자로 배달됩니다.  
  
```  
CREATE REMOTE SERVICE BINDING APBinding  
    TO SERVICE '//Adventure-Works.com/services/AccountsPayable'  
    WITH USER = APUser, ANONYMOUS=ON ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/alter-remote-service-binding-transact-sql.md)   
 [DROP REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/drop-remote-service-binding-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
