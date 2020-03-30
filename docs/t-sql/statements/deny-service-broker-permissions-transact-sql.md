---
title: DENY Service Broker 사용 권한(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/09/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- denying permissions [Service Broker]
- routes [Service Broker], permissions
- Service Broker, permissions
- DENY statement, Service Broker
- remote service bindings [Service Broker], permissions
- permissions [Service Broker]
- message types [Service Broker], permissions
- denying permissions [SQL Server], Service Broker
- contracts [Service Broker], permissions
- services [Service Broker], permissions
ms.assetid: 7c6de71b-865c-41db-9413-ad9b3562e579
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 346044530087c40c468abe9d304231ce06220845
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67984428"
---
# <a name="deny-service-broker-permissions-transact-sql"></a>DENY Service Broker 권한(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 계약, 메시지 유형, 원격 서비스 바인딩, 경로 또는 서비스에 대한 사용 권한을 거부합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
DENY permission  [ ,...n ] ON  
    {    
       [ CONTRACT :: contract_name ]   
       | [ MESSAGE TYPE :: message_type_name ]    
       | [ REMOTE SERVICE BINDING :: remote_binding_name ]    
       | [ ROUTE :: route_name ]   
       | [ SERVICE :: service_name ]      
        }  
    TO database_principal [ ,...n ]   
    [ CASCADE ]  
        [ AS denying_principal ]  
```  
  
## <a name="arguments"></a>인수  
 *permission*  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 보안 개체에 대해 거부할 수 있는 사용 권한을 지정합니다. 사용 권한 목록은 이 항목의 뒤에 나오는 주의 섹션을 참조하세요.  
  
 CONTRACT **::** _contract_name_  
 사용 권한을 거부할 계약을 지정합니다. 범위 한정자 **::** 가 필요합니다.  
  
 MESSAGE TYPE **::** _message_type_name_  
 사용 권한을 거부할 메시지 유형을 지정합니다. 범위 한정자 **::** 가 필요합니다.  
  
 REMOTE SERVICE BINDING **::** _remote_binding_name_  
 사용 권한을 거부할 원격 서비스 바인딩을 지정합니다. 범위 한정자 **::** 가 필요합니다.  
  
 ROUTE **::** _route_name_  
 사용 권한을 거부할 경로를 지정합니다. 범위 한정자 **::** 가 필요합니다.  
  
 SERVICE **::** _message_type_name_  
 사용 권한을 거부할 서비스를 지정합니다. 범위 한정자 **::** 가 필요합니다.  
  
 *database_principal*  
 사용 권한을 거부할 보안 주체를 지정합니다. 다음 중 하나  
  
-   데이터베이스 사용자  
-   데이터베이스 역할  
-   애플리케이션 역할  
-   Windows 로그인에 매핑된 데이터베이스 사용자  
-   Windows 그룹에 매핑된 데이터베이스 사용자  
-   인증서에 매핑된 데이터베이스 사용자  
-   비대칭 키에 매핑된 데이터베이스 사용자  
-   서버 보안 주체로 매핑되지 않은 데이터베이스 사용자  
  
CASCADE  
 사용 권한이 거부된 보안 주체에게 사용 권한을 부여 받은 다른 보안 주체의 사용 권한도 거부됨을 나타냅니다.  
  
*denying_principal*  
 이 쿼리를 실행하는 보안 주체가 사용 권한을 거부하는 권한을 부여할 수 있는 다른 보안 주체를 지정합니다. 다음 중 하나  
  
-   데이터베이스 사용자  
-   데이터베이스 역할  
-   애플리케이션 역할  
-   Windows 로그인에 매핑된 데이터베이스 사용자  
-   Windows 그룹에 매핑된 데이터베이스 사용자  
-   인증서에 매핑된 데이터베이스 사용자  
-   비대칭 키에 매핑된 데이터베이스 사용자  
-   서버 보안 주체로 매핑되지 않은 데이터베이스 사용자  
  
## <a name="remarks"></a>설명  
  
## <a name="service-broker-contracts"></a>Service Broker 계약  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 계약은 사용 권한 계층에서 부모 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 다음 표에는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 계약에 대해 거부할 수 있는 가장 제한적인 사용 권한이 해당 사용 권한을 암시적으로 포함하는 보다 일반적인 사용 권한과 함께 정리되어 있습니다.  
  
|Service Broker 계약 권한|Service Broker 계약 권한에 포함된 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|----------------------------------------|---------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY CONTRACT|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-message-types"></a>Service Broker 메시지 유형  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 메시지 유형은 사용 권한 계층에서 부모 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 다음 표에는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 메시지 유형에 대해 거부할 수 있는 가장 제한적인 사용 권한이 해당 사용 권한을 암시적으로 포함하는 보다 일반적인 사용 권한과 함께 정리되어 있습니다.  
  
|Service Broker 메시지 유형 권한|Service Broker 메시지 유형 권한에 포함된 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|--------------------------------------------|-------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY MESSAGE TYPE|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-remote-service-bindings"></a>Service Broker 원격 서비스 바인딩  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 원격 서비스 바인딩은 사용 권한 계층에서 부모 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 다음 표에는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 원격 서비스 바인딩에 대해 거부할 수 있는 가장 제한적인 사용 권한이 해당 사용 권한을 암시적으로 포함하는 보다 일반적인 사용 권한과 함께 정리되어 있습니다.  
  
|Service Broker 원격 서비스 바인딩 권한|Service Broker 원격 서비스 바인딩 권한에 포함된 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|------------------------------------------------------|-----------------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY REMOTE SERVICE BINDING|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-routes"></a>Service Broker 경로  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 경로는 사용 권한 계층에서 부모 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 다음 표에는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 경로에 대해 거부할 수 있는 가장 제한적인 사용 권한이 해당 사용 권한을 암시적으로 포함하는 보다 일반적인 사용 권한과 함께 정리되어 있습니다.  
  
|Service Broker 경로 권한|Service Broker 경로 권한에 포함된 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|-------------------------------------|------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ROUTE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
### <a name="service-broker-services"></a>Service Broker 서비스  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 서비스는 사용 권한 계층에서 부모 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 다음 표에는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 서비스에 대해 거부할 수 있는 가장 제한적인 사용 권한이 해당 사용 권한을 암시적으로 포함하는 보다 일반적인 사용 권한과 함께 정리되어 있습니다.  
  
|Service Broker 서비스 권한|Service Broker 서비스 권한에 포함된 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|---------------------------------------|--------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|SEND|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY SERVICE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 계약, 메시지 유형, 원격 서비스 바인딩, 경로 또는 서비스에 대한 CONTROL 권한이 필요합니다. AS 절을 사용하는 경우 지정된 보안 주체가 사용 권한을 거부할 보안 개체를 소유해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [REVOKE Service Broker 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)   
 [DENY&#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)  
  
  
