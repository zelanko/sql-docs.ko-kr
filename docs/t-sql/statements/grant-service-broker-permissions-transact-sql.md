---
title: "GRANT Service Broker 권한 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- granting permissions [SQL Server], Service Broker
- routes [Service Broker], permissions
- Service Broker, permissions
- GRANT statement, Service Broker
- remote service bindings [Service Broker], permissions
- message types [Service Broker], permissions
- contracts [Service Broker], permissions
ms.assetid: c5579976-97c4-4123-be0c-d0b98a9e38fb
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 185950b1872ca5f11663f3d5051d1a2303cce090
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="grant-service-broker-permissions-transact-sql"></a>GRANT Service Broker 권한(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Service Broker 계약, 메시지 유형, 원격 바인딩, 경로 또는 서비스에 대한 사용 권한을 부여합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
GRANT permission  [ ,...n ] ON  
    {    
              [ CONTRACT :: contract_name ]   
       | [ MESSAGE TYPE :: message_type_name ]    
       | [ REMOTE SERVICE BINDING :: remote_binding_name ]    
       | [ ROUTE :: route_name ]   
       | [ SERVICE :: service_name ]      
    }  
    TO database_principal [ ,...n ]   
    [ WITH GRANT OPTION ]  
        [ AS granting_principal ]  
```  
  
## <a name="arguments"></a>인수  
 *사용 권한*  
 Service Broker 보안 개체에 부여할 수 있는 사용 권한을 지정합니다.  아래와 같습니다.  
  
 계약 **::***contract_name*  
 사용 권한을 부여할 계약을 지정합니다. 범위 한정자 "::"가 필요 합니다.  
  
 메시지 유형 **::***message_type_name*  
 사용 권한을 부여할 메시지 유형을 지정합니다. 범위 한정자 "::"이 필요합니다.  
  
 REMOTE SERVICE BINDING **::***remote_binding_name*  
 사용 권한을 부여할 원격 서비스 바인딩을 지정합니다. 범위 한정자 "::"이 필요합니다.  
  
 경로 **::***route_name*  
 사용 권한을 부여할 경로를 지정합니다. 범위 한정자 "::"이 필요합니다.  
  
 서비스 **::***service_name*  
 사용 권한을 부여할 서비스를 지정합니다. 범위 한정자 "::"이 필요합니다.  
  
 *데이터베이스 _ 보안 주체*  
 사용 권한을 부여할 보안 주체를 지정합니다. 다음 중 하나일 수 있습니다.  
  
-   데이터베이스 사용자  
  
-   데이터베이스 역할  
  
-   응용 프로그램 역할  
  
-   Windows 로그인에 매핑된 데이터베이스 사용자  
  
-   Windows 그룹에 매핑된 데이터베이스 사용자  
  
-   인증서에 매핑된 데이터베이스 사용자  
  
-   비대칭 키에 매핑된 데이터베이스 사용자  
  
-   서버 보안 주체에 매핑되지 않은 데이터베이스 사용자  
  
 GRANT OPTION  
 지정된 사용 권한을 다른 보안 주체에게 부여할 수 있는 권한도 이 보안 주체에 제공됨을 나타냅니다.  
  
 *granting_principal*  
 이 쿼리를 실행하는 보안 주체가 사용 권한을 부여하는 권한을 부여할 수 있는 다른 보안 주체를 지정합니다. 다음 중 하나일 수 있습니다.  
  
-   데이터베이스 사용자  
  
-   데이터베이스 역할  
  
-   응용 프로그램 역할  
  
-   Windows 로그인에 매핑된 데이터베이스 사용자  
  
-   Windows 그룹에 매핑된 데이터베이스 사용자  
  
-   인증서에 매핑된 데이터베이스 사용자  
  
-   비대칭 키에 매핑된 데이터베이스 사용자  
  
-   서버 보안 주체에 매핑되지 않은 데이터베이스 사용자  
  
## <a name="remarks"></a>주의  
  
## <a name="service-broker-contracts"></a>Service Broker 계약  
 Service Broker 계약은 사용 권한 계층에서 부모 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 아래에는 Service Broker 계약에 부여할 수 있는 가장 제한적인 사용 권한이 이러한 권한을 암시적으로 포함하는 보다 일반적인 사용 권한과 함께 정리되어 있습니다.  
  
|Service Broker 계약 권한|Service Broker 계약 권한에 포함된 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|----------------------------------------|---------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY CONTRACT|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-message-types"></a>Service Broker 메시지 유형  
 Service Broker 메시지 유형은 사용 권한 계층에서 부모 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 아래에는 Service Broker 메시지 유형에 부여할 수 있는 가장 제한적인 사용 권한이 이러한 권한을 암시적으로 포함하는 보다 일반적인 사용 권한과 함께 정리되어 있습니다.  
  
|Service Broker 메시지 유형 권한|Service Broker 메시지 유형 권한에 포함된 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|--------------------------------------------|-------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY MESSAGE TYPE|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-remote-service-bindings"></a>Service Broker 원격 서비스 바인딩  
 Service Broker 원격 서비스 바인딩은 사용 권한 계층에서 부모 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 아래에는 Service Broker 원격 서비스 바인딩에 부여할 수 있는 가장 제한적인 사용 권한이 이러한 권한을 암시적으로 포함하는 보다 일반적인 사용 권한과 함께 정리되어 있습니다.  
  
|Service Broker 원격 서비스 바인딩 권한|Service Broker 원격 서비스 바인딩 권한에 포함된 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|------------------------------------------------------|-----------------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY REMOTE SERVICE BINDING|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-routes"></a>Service Broker 경로  
 Service Broker 경로는 사용 권한 계층에서 부모 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 아래에는 Service Broker 경로에 부여할 수 있는 가장 제한적인 사용 권한이 이러한 권한을 암시적으로 포함하는 보다 일반적인 사용 권한과 함께 정리되어 있습니다.  
  
|Service Broker 경로 권한|Service Broker 경로 권한에 포함된 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|-------------------------------------|------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ROUTE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
### <a name="service-broker-services"></a>Service Broker 서비스  
 Service Broker 서비스는 사용 권한 계층에서 부모 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 아래에는 Service Broker 서비스에 부여할 수 있는 가장 제한적인 사용 권한이 이러한 권한을 암시적으로 포함하는 보다 일반적인 사용 권한과 함께 정리되어 있습니다.  
  
|Service Broker 서비스 권한|Service Broker 서비스 권한에 포함된 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|---------------------------------------|--------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|SEND|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY SERVICE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 사용 권한을 부여한 사용자 또는 AS 옵션으로 지정한 보안 주체에게 GRANT OPTION을 통한 사용 권한이 있거나 부여할 사용 권한을 포함하는 상위 사용 권한이 있어야 합니다.  
  
 AS 옵션을 사용하는 경우 다음과 같은 추가 요구 사항이 적용됩니다.  
  
|AS *granting_principal*|필요한 추가 사용 권한|  
|------------------------------|------------------------------------|  
|데이터베이스 사용자|멤버 자격 사용자에 대 한 IMPERSONATE 권한이 **db_securityadmin** 고정된 데이터베이스 역할의 멤버 자격는 **db_owner** 고정 데이터베이스 역할의 멤버 자격이 **sysadmin** 고정된 서버 역할입니다.|  
|Windows 로그인에 매핑된 데이터베이스 사용자|멤버 자격 사용자에 대 한 IMPERSONATE 권한이 **db_securityadmin** 고정된 데이터베이스 역할의 멤버 자격는 **db_owner** 고정 데이터베이스 역할의 멤버 자격이 **sysadmin** 고정된 서버 역할입니다.|  
|Windows 그룹에 매핑된 데이터베이스 사용자|Windows 그룹의 멤버 자격이 **db_securityadmin** 고정된 데이터베이스 역할의 멤버 자격는 **db_owner** 고정 데이터베이스 역할의 멤버 자격이 **sysadmin**고정된 서버 역할입니다.|  
|인증서에 매핑된 데이터베이스 사용자|멤버 자격이 **db_securityadmin** 고정된 데이터베이스 역할의 멤버 자격는 **db_owner** 고정 데이터베이스 역할의 멤버 자격이 **sysadmin** 고정된 서버 역할입니다.|  
|비대칭 키에 매핑된 데이터베이스 사용자|멤버 자격이 **db_securityadmin** 고정된 데이터베이스 역할의 멤버 자격는 **db_owner** 고정 데이터베이스 역할의 멤버 자격이 **sysadmin** 고정된 서버 역할입니다.|  
|서버 보안 주체에 매핑되지 않은 데이터베이스 사용자|멤버 자격 사용자에 대 한 IMPERSONATE 권한이 **db_securityadmin** 고정된 데이터베이스 역할의 멤버 자격는 **db_owner** 고정 데이터베이스 역할의 멤버 자격이 **sysadmin** 고정된 서버 역할입니다.|  
|데이터베이스 역할|역할의 멤버 자격에 대 한 ALTER 권한이 **db_securityadmin** 고정된 데이터베이스 역할의 멤버 자격는 **db_owner** 고정 데이터베이스 역할의 멤버 자격이 **sysadmin**고정된 서버 역할입니다.|  
|응용 프로그램 역할|역할의 멤버 자격에 대 한 ALTER 권한이 **db_securityadmin** 고정된 데이터베이스 역할의 멤버 자격는 **db_owner** 고정 데이터베이스 역할의 멤버 자격이 **sysadmin**고정된 서버 역할입니다.|  
  
 개체 소유자는 소유하고 있는 개체에 대한 사용 권한을 부여할 수 있습니다. 보안 개체에 대한 CONTROL 사용 권한을 가진 보안 주체는 해당 보안 개체에 대한 사용 권한을 부여할 수 있습니다.  
  
 멤버와 같이 CONTROL SERVER 권한이 부여 된 사용자는 **sysadmin** 고정된 서버 역할에 대 한 사용 권한을 부여할 수 있습니다는 서버 보안 개체입니다. 한의 멤버와 같이 데이터베이스에 대 한 CONTROL 권한이 **db_owner** 고정된 데이터베이스 역할에 대 한 사용 권한을 부여할 수는 데이터베이스 보안 개체입니다. 스키마에 대한 CONTROL 권한이 부여된 사용자는 스키마 내의 모든 개체에 대한 사용 권한을 부여할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

