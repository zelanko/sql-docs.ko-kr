---
title: "REVOKE Service Broker 권한 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- routes [Service Broker], permissions
- Service Broker, permissions
- remote service bindings [Service Broker], permissions
- permissions [Service Broker]
- message types [Service Broker], permissions
- contracts [Service Broker], permissions
- services [Service Broker], permissions
- REVOKE statement, Service Broker
ms.assetid: 70f1d938-97e2-48a4-9bc0-8be9f2f2c36d
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 077fe296f48de1658a56d0c3e7403904652603bc
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="revoke-service-broker-permissions-transact-sql"></a>REVOKE Service Broker 권한(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 계약, 메시지 유형, 원격 서비스 바인딩, 경로 또는 서비스에 대한 사용 권한을 취소합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ] ON  
    {   
       [ CONTRACT :: contract_name ]   
       | [ MESSAGE TYPE :: message_type_name ]    
       | [ REMOTE SERVICE BINDING :: remote_binding_name ]    
       | [ ROUTE :: route_name ]   
       | [ SERVICE :: service_name ]      
        }  
    { TO | FROM } database_principal [ ,...n ]  
    [ CASCADE ]  
    [ AS revoking_principal ]  
```  
  
## <a name="arguments"></a>인수  
 GRANT OPTION FOR  
 지정된 권한을 다른 보안 주체에게 부여할 수 있는 권한이 취소됨을 나타냅니다. 사용 권한 자체는 취소되지 않습니다.  
  
> [!IMPORTANT]  
>  보안 주체에 GRANT 옵션 없이 지정된 사용 권한이 있는 경우 사용 권한 자체가 취소됩니다.  
  
 *사용 권한*  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 보안 개체에 대해 취소할 수 있는 사용 권한을 지정합니다. 사용 권한 목록은 이 항목의 뒤에 나오는 주의 섹션을 참조하세요.  
  
 계약 **::***contract_name*  
 사용 권한을 취소할 계약을 지정합니다. 범위 한정자 **::** 가 필요 합니다.  
  
 메시지 유형 **::***message_type_name*  
 사용 권한을 취소할 메시지 유형을 지정합니다. 범위 한정자 **::** 가 필요 합니다.  
  
 REMOTE SERVICE BINDING **::***remote_binding_name*  
 사용 권한을 취소할 원격 서비스 바인딩을 지정합니다. 범위 한정자 **::** 가 필요 합니다.  
  
 경로 **::***route_name*  
 사용 권한을 취소할 경로를 지정합니다. 범위 한정자 **::** 가 필요 합니다.  
  
 서비스 **::***message_type_name*  
 사용 권한을 취소할 서비스를 지정합니다. 범위 한정자 **::** 가 필요 합니다.  
  
 *데이터베이스 _ 보안 주체*  
 사용 권한을 취소할 보안 주체를 지정합니다. *데이터베이스 _ 보안 주체* 다음 중 하나일 수 있습니다.  
  
-   데이터베이스 사용자  
  
-   데이터베이스 역할  
  
-   응용 프로그램 역할  
  
-   Windows 로그인에 매핑된 데이터베이스 사용자  
  
-   Windows 그룹에 매핑된 데이터베이스 사용자  
  
-   인증서에 매핑된 데이터베이스 사용자  
  
-   비대칭 키에 매핑된 데이터베이스 사용자  
  
-   서버 보안 주체로 매핑되지 않은 데이터베이스 사용자  
  
 CASCADE  
 사용 권한이 취소된 보안 주체에게 사용 권한을 부여 받거나 거부당한 다른 보안 주체의 사용 권한도 취소됨을 나타냅니다.  
  
> [!CAUTION]  
>  WITH GRANT OPTION을 부여 받은 사용 권한이 연계되어 취소되면 해당 사용 권한의 GRANT 및 DENY가 모두 취소됩니다.  
  
 AS *revoking_principal*  
 이 쿼리를 실행하는 보안 주체가 사용 권한을 취소하는 권한을 부여할 수 있는 다른 보안 주체를 지정합니다. *revoking_principal* 다음 중 하나일 수 있습니다.  
  
-   데이터베이스 사용자  
  
-   데이터베이스 역할  
  
-   응용 프로그램 역할  
  
-   Windows 로그인에 매핑된 데이터베이스 사용자  
  
-   Windows 그룹에 매핑된 데이터베이스 사용자  
  
-   인증서에 매핑된 데이터베이스 사용자  
  
-   비대칭 키에 매핑된 데이터베이스 사용자  
  
-   서버 보안 주체로 매핑되지 않은 데이터베이스 사용자  
  
## <a name="remarks"></a>주의  
  
## <a name="service-broker-contracts"></a>Service Broker 계약  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 계약은 사용 권한 계층에서 부모 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 가장 제한적인된 특정 사용 권한이에 대해 취소할 수 있는 한 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 계약 암시적으로 포함 하는 보다 일반적인 사용 권한과 함께 다음 표에 나열 됩니다.  
  
|Service Broker 계약 권한|Service Broker 계약 권한에 포함된 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|----------------------------------------|---------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY CONTRACT|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-message-types"></a>Service Broker 메시지 유형  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 메시지 유형은 사용 권한 계층에서 부모 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 다음 표에서는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 메시지 유형에 대해 취소할 수 있는 가장 제한적인 사용 권한과 의미상 이러한 사용 권한을 포함하는 보다 일반적인 사용 권한을 나열합니다.  
  
|Service Broker 메시지 유형 권한|Service Broker 메시지 유형 권한에 포함된 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|--------------------------------------------|-------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY MESSAGE TYPE|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-remote-service-bindings"></a>Service Broker 원격 서비스 바인딩  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 원격 서비스 바인딩은 사용 권한 계층에서 부모 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 다음 표에서는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 원격 서비스 바인딩에 대해 취소할 수 있는 가장 제한적인 사용 권한과 의미상 이러한 사용 권한을 포함하는 보다 일반적인 사용 권한을 나열합니다.  
  
|Service Broker 원격 서비스 바인딩 권한|Service Broker 원격 서비스 바인딩 권한에 포함된 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|------------------------------------------------------|-----------------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY REMOTE SERVICE BINDING|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-routes"></a>Service Broker 경로  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 경로는 사용 권한 계층에서 부모 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 가장 제한적인된 특정 사용 권한이에 대해 취소할 수 있는 한 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 경로 암시적으로 포함 하는 보다 일반적인 사용 권한과 함께 다음 표에 나열 됩니다.  
  
|Service Broker 경로 권한|Service Broker 경로 권한에 포함된 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|-------------------------------------|------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ROUTE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
### <a name="service-broker-services"></a>Service Broker 서비스  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 서비스는 사용 권한 계층에서 부모 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 가장 제한적인된 특정 사용 권한이에 대해 취소할 수 있는 한 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 서비스 암시적으로 포함 하는 보다 일반적인 사용 권한과 함께 다음 표에 나열 됩니다.  
  
|Service Broker 서비스 권한|Service Broker 서비스 권한에 포함된 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|---------------------------------------|--------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|SEND|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY SERVICE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 계약, 메시지 유형, 원격 서비스 바인딩, 경로 또는 서비스에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [GRANT Service Broker 사용 권한 &#40; Transact SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)   
 [Service Broker 권한 &#40; 거부 Transact SQL &#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)   
 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
