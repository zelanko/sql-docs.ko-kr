---
title: "끝점 (Transact SQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ENDPOINT
- CREATE ENDPOINT
- ENDPOINT_TSQL
- CREATE_ENDPOINT_TSQL
dev_langs: TSQL
helpviewer_keywords:
- database mirroring [SQL Server], endpoint
- HTTP SOAP support [SQL Server]
- CREATE ENDPOINT statement
- Availability Groups [SQL Server], configuring
- endpoints [SQL Server], creating
- SOAP [SQL Server built-in support], endpoints
- SOAP [SQL Server built-in support], sqlbatch
- DATABASE_MIRRORING option
- HTTP protocol option [SQL Server]
- SOAP [SQL Server built-in support], ad hoc
- TCP protocol option [SQL Server]
- SERVICE_BROKER option
- Availability Groups [SQL Server], endpoint
ms.assetid: 6405e7ec-0b5b-4afd-9792-1bfa5a2491f6
caps.latest.revision: "135"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a8ce3df8a9b6e7ead8e775b6bd0b2d31720b38a9
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="create-endpoint-transact-sql"></a>CREATE ENDPOINT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  클라이언트 응용 프로그램에 사용할 수 있는 메서드를 포함하여 끝점을 만들고 속성을 정의합니다. 관련된 사용 권한 정보를 참조 하십시오. [GRANT 끝점 사용 권한 &#40; Transact SQL &#41; ](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md).  
  
 CREATE ENDPOINT의 구문은 논리적으로 다음과 같이 두 부분으로 나눌 수 있습니다.  
  
-   첫 번째 부분은 AS로 시작하고 FOR 절 앞에서 끝납니다.  
  
     이 부분에서는 전송 프로토콜(TCP)과 관련된 정보를 제공하며 끝점의 수신 포트 번호를 설정하고 끝점 인증 방법 및/또는 끝점에 대한 액세스를 차단할 IP 주소(있는 경우) 목록을 설정합니다.  
  
-   두 번째 부분은 FOR 절로 시작합니다.  
  
     이 부분에서는 끝점에서 지원되는 페이로드를 정의합니다. 페이로드는 지원 되는 여러 가지 유형 중 하나일 수 있습니다: [!INCLUDE[tsql](../../includes/tsql-md.md)], service broker, 미러링 데이터베이스. 또한 이 부분에는 언어별 정보도 포함됩니다.  
  
> **참고:** 네이티브 XML 웹 서비스 (SOAP/HTTP 끝점)에서 제거 되었던 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
CREATE ENDPOINT endPointName [ AUTHORIZATION login ]  
[ STATE = { STARTED | STOPPED | DISABLED } ]  
AS { TCP } (  
   <protocol_specific_arguments>  
        )  
FOR { TSQL | SERVICE_BROKER | DATABASE_MIRRORING } (  
   <language_specific_arguments>  
        )  
  
<AS TCP_protocol_specific_arguments> ::=  
AS TCP (  
  LISTENER_PORT = listenerPort  
  [ [ , ] LISTENER_IP = ALL | ( 4-part-ip ) | ( "ip_address_v6" ) ]  
  
)  
  
<FOR SERVICE_BROKER_language_specific_arguments> ::=  
FOR SERVICE_BROKER (  
   [ AUTHENTICATION = {   
            WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
      | CERTIFICATE certificate_name   
      | WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ] CERTIFICATE certificate_name   
      | CERTIFICATE certificate_name WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
    } ]  
   [ [ , ] ENCRYPTION = { DISABLED | { { SUPPORTED | REQUIRED }   
       [ ALGORITHM { AES | RC4 | AES RC4 | RC4 AES } ] }   
   ]  
   [ [ , ] MESSAGE_FORWARDING = { ENABLED | DISABLED } ]  
   [ [ , ] MESSAGE_FORWARD_SIZE = forward_size ]  
)  
  

<FOR DATABASE_MIRRORING_language_specific_arguments> ::=  
FOR DATABASE_MIRRORING (  
   [ AUTHENTICATION = {   
            WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
      | CERTIFICATE certificate_name   
      | WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ] CERTIFICATE certificate_name   
      | CERTIFICATE certificate_name WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
   [ [ [ , ] ] ENCRYPTION = { DISABLED | { { SUPPORTED | REQUIRED }   
       [ ALGORITHM { AES | RC4 | AES RC4 | RC4 AES } ] }   
  
    ]   
   [ , ] ROLE = { WITNESS | PARTNER | ALL }  
)  
```  
  
## <a name="arguments"></a>인수  
 *endPointName*  
 만들어지는 끝점에 할당할 이름입니다. 끝점을 업데이트하거나 삭제할 때 사용합니다.  
  
 권한 부여 *로그인*  
 새로 만들어지는 끝점 개체의 소유권을 할당할 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Windows 로그인을 지정합니다. AUTHORIZATION이 지정되지 않은 경우 기본적으로 호출자가 새로 만들어지는 개체의 소유자가 됩니다.  
  
 권한 부여를 지정 하 여 소유권을 할당 하려면 호출자에 게 있어야 대 한 IMPERSONATE 권한이 지정 된 *로그인*합니다.  
  
 소유권을 다시 할당 참조 [ALTER endpoint&#40; Transact SQL &#41; ](../../t-sql/statements/alter-endpoint-transact-sql.md).  
  
 상태  **=**  {시작 됨 | **STOPPED** | (를) 사용 안 함  
 끝점이 생성될 때의 끝점 상태입니다. 끝점을 만들 때 상태를 지정하지 않으면 STOPPED가 기본값이 됩니다.  
  
 STARTED  
 끝점이 시작되어 연결 수신 대기 중입니다.  
  
 DISABLED  
 끝점이 해제되었습니다. 이 상태일 경우 서버는 포트 요청을 수신하지만 오류를 클라이언트에 반환합니다.  
  
 **중지 됨**  
 끝점이 중지되었습니다. 이 상태에서 서버는 끝점 포트로의 수신을 대기하거나 끝점을 사용하기 위해 시도된 요청에 응답하지 않습니다.  
  
 상태를 변경 하려면 사용 [ALTER endpoint&#40; Transact SQL &#41; ](../../t-sql/statements/alter-endpoint-transact-sql.md).  
  
 AS { TCP }  
 사용할 전송 프로토콜을 지정합니다.  
  
 FOR { TSQL | SERVICE_BROKER | DATABASE_MIRRORING }  
 페이로드 유형을 지정합니다.  
  
 현재 `<language_specific_arguments>` 매개 변수에 전달할 [!INCLUDE[tsql](../../includes/tsql-md.md)] 언어 관련 인수는 없습니다.  
  
 **TCP 프로토콜 옵션**  
  
 다음 인수는 TCP 프로토콜 옵션에만 적용됩니다.  
  
 LISTENER_PORT  **=**  *listenerPort*  
 Service Broker TCP/IP 프로토콜을 통한 연결을 수신하는 포트 번호를 지정합니다. 규칙에 따라 4022가 사용되지만 1024와 32767 사이의 모든 번호를 사용할 수 있습니다.  
  
 LISTENER_IP  **=**  모든 | **(***4 부분 ip* **)** | **(** "*ip_address_v6*"  **)**  
 끝점이 수신하는 IP 주소를 지정합니다. 기본값은 ALL입니다. 이는 수신기가 모든 유효한 IP 주소에 대한 연결을 허용함을 의미합니다.  
  
 정규화된 도메인 이름(`ALTER DATABASE SET PARTNER = partner_IP_address` 또는 `ALTER DATABASE SET WITNESS = witness_IP_address`) 대신 IP 주소를 사용하여 데이터베이스 미러링을 구성하는 경우 미러링 끝점을 만들 때 `LISTENER_IP =IP_address` 대신 `LISTENER_IP=ALL`를 지정해야 합니다.  
  
 **SERVICE_BROKER 및 DATABASE_MIRRORING 옵션**  
  
 다음 AUTHENTICATION 및 ENCRYPTION 인수는 SERVICE_BROKER 및 DATABASE_MIRRORING 옵션에 사용할 수 있는 공통 인수입니다.  
  
> [!NOTE]  
>  SERVICE_BROKER와 관련된 옵션은 이 섹션 뒷부분의 "SERVICE_BROKER 옵션"을 참조하십시오. DATABASE_MIRRORING과 관련된 옵션은 이 섹션 뒷부분의 "DATABASE_MIRRORING 옵션"을 참조하십시오.  
  
 인증  **=**  \<authentication_options >이 끝점에 대 한 연결에 대 한 TCP/IP 인증 요구 사항을 지정 합니다. 기본값은 WINDOWS입니다.  
  
 지원되는 인증 방법에는 NTLM 또는 Kerberos가 있으며 둘 다 사용할 수도 있습니다.  
  
> [!IMPORTANT]  
>  서버 인스턴스의 모든 미러링 연결은 하나의 데이터베이스 미러링 끝점을 사용합니다. 추가 데이터베이스 미러링 끝점을 만들려고 시도하면 실패합니다.  
  
 **\<authentication_options >:: =**  
  
 **WINDOWS** [{NTLM | KERBEROS | **NEGOTIATE** }]  
 끝점이 인증을 위해 Windows 인증 프로토콜을 사용하여 연결하도록 지정합니다. 기본값입니다.  
  
 인증 방법(NTLM 또는 KERBEROS)을 지정한 경우 항상 해당 방법이 인증 프로토콜로 사용됩니다. 기본값인 NEGOTIATE를 적용하면 끝점이 Windows 협상 프로토콜을 사용하여 NTLM이나 Kerberos를 선택합니다.  
  
 인증서 *certificate_name*  
 으로 지정 된 인증서를 사용 하 여 연결을 인증 하는 끝점 임을 지정 *certificate_name* 권한 부여에 대 한 id를 설정 합니다. 먼 끝점에는 지정된 인증서의 개인 키와 일치하는 공개 키를 가진 인증서가 있어야 합니다.  
  
 WINDOWS [{NTLM | KERBEROS | **NEGOTIATE** }] 인증서 *certificate_name*  
 Windows 인증을 사용하여 끝점이 연결을 시도하고 이 시도가 실패하면 지정한 인증서를 사용하여 연결을 시도하도록 지정합니다.  
  
 인증서 *certificate_name* WINDOWS [{NTLM | KERBEROS | **NEGOTIATE** }]  
 지정한 인증서를 사용하여 끝점이 연결을 시도하고 이 시도가 실패하면 Windows 인증을 사용하여 연결을 시도하도록 지정합니다.  
  
 암호화 = {사용 안 함 | 지원 | **REQUIRED** } [알고리즘 { **AES** | RC4 | AES R C 4 | RC4 AES}]  
 프로세스에서 암호화를 사용할지 여부를 지정합니다. 기본값은 REQUIRED입니다.  
  
 DISABLED  
 연결을 통해 전송되는 데이터를 암호화하지 않도록 지정합니다.  
  
 SUPPORTED  
 반대쪽 끝점이 SUPPORTED나 REQUIRED로 지정된 경우에만 데이터를 암호화하도록 지정합니다.  
  
 REQUIRED  
 이 끝점에 대한 연결이 암호화를 사용하도록 지정합니다. 따라서 이 끝점에 연결하려면 다른 끝점의 ENCRYPTION이 SUPPORTED 또는 REQUIRED로 설정되어 있어야 합니다.  
  
 필요에 따라 다음과 같이 ALGORITHM 인수를 사용하여 끝점에 사용되는 암호화 형식을 지정할 수 있습니다.  
  
 **AES**  
 끝점이 반드시 AES 알고리즘을 반드시 사용하도록 지정합니다. 이 대화 상자에서 기본 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상.  
  
 RC4  
 끝점이 반드시 RC4 알고리즘을 사용하도록 지정합니다. 이 통해 기본값 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]합니다.  
  
> [!NOTE]  
>  RC4 알고리즘은 이전 버전과의 호환성을 위해서만 지원됩니다. 데이터베이스의 호환성 수준이 90 또는 100인 경우 새 자료는 RC4 또는 RC4_128로만 암호화할 수 있습니다. 이 옵션은 사용하지 않는 것이 좋습니다. 대신 AES 알고리즘 중 하나와 같은 새 알고리즘을 사용하십시오. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상 버전에서 RC4 또는 RC4_128을 사용하여 암호화된 자료는 모든 호환성 수준에서 해독할 수 있습니다.  
  
 AES RC4  
 두 끝점이 암호화 알고리즘에 대해 협상하고 이 끝점이 AES 알고리즘에 우선권을 주도록 지정합니다.  
  
 RC4 AES  
 두 끝점이 암호화 알고리즘에 대해 협상하고 이 끝점이 RC4 알고리즘에 우선권을 주도록 지정합니다.  
  
> [!NOTE]  
>  RC4 알고리즘은 더 이상 사용되지 않습니다. [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] AES를 사용하는 것이 좋습니다.  
  
 양쪽 끝점이 두 알고리즘을 모두 지정하지만 순서가 다른 경우 연결을 수락하는 끝점의 알고리즘이 적용됩니다.  
  
 **SERVICE_BROKER 옵션**  
  
 다음은 SERVICE_BROKER 옵션에 대한 인수입니다.  
  
 MESSAGE_FORWARDING  **=**  {사용 | **비활성화** }  
 끝점에서 수신한 메시지가 다른 위치에 있는 서비스에 관련된 것일 경우 이 메시지를 전달할지 여부를 결정합니다.  
  
 ENABLED  
 전달 주소가 있을 경우 메시지를 전달합니다.  
  
 DISABLED  
 다른 위치에 있는 서비스에 대한 메시지를 무시합니다. 기본값입니다.  
  
 MESSAGE_FORWARD_SIZE  **=**  *forward_size*  
 끝점이 전달할 메시지를 저장할 때 사용할 수 있는 최대 저장 크기(MB)를 지정합니다.  
  
 **DATABASE_MIRRORING 옵션**  
  
 다음은 DATABASE_MIRRORING 옵션에 대한 인수입니다.  
  
 역할  **=**  {미러링 모니터 서버 | 파트너 | 모든}  
 데이터베이스 미러링 역할 또는 끝점이 지원하는 역할을 지정합니다.  
  
 WITNESS  
 미러링 프로세스에서 끝점이 미러링 모니터의 역할을 수행하도록 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)]의 경우 WITNESS 옵션만 사용할 수 있습니다.  
  
 PARTNER  
 미러링 프로세스에서 끝점이 파트너의 역할을 수행하도록 합니다.  
  
 ALL  
 미러링 프로세스에서 끝점이 미러링 모니터 및 파트너 역할을 모두 수행하도록 지정합니다.  
  
 이러한 역할에 대 한 자세한 내용은 참조 하십시오. [데이터베이스 미러링 &#40; SQL Server &#41; ](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
> [!NOTE]  
>  DATABASE_MIRRORING에 대한 기본 포트는 없습니다.  
  
## <a name="remarks"></a>주의  
 ENDPOINT DDL 문은 사용자 트랜잭션 내에서 실행할 수 없습니다. 활성 스냅숏 격리 수준 트랜잭션이 변경되는 끝점을 사용하는 경우에도 ENDPOINT DDL 문은 실패하지 않습니다.  
  
 ENDPOINT에 대한 요청을 실행할 수 있는 사람은 다음과 같습니다.  
  
-   멤버 **sysadmin** 고정된 서버 역할  
  
-   끝점의 소유자  
  
-   끝점에 대한 CONNECT 권한이 부여된 사용자 또는 그룹  
  
## <a name="permissions"></a>Permissions  
 CREATE ENDPOINT 권한 또는 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다. 자세한 내용은 [GRANT 끝점 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)을 참조하세요.  
  
## <a name="example"></a>예제  
  
### <a name="creating-a-database-mirroring-endpoint"></a>데이터베이스 미러링 끝점 만들기  
 다음 예에서는 데이터베이스 미러링 끝점을 만듭니다. 사용할 수 있는 포트 번호라면 어떤 것이라도 관계 없으나 여기서는 끝점이 `7022` 포트 번호를 사용합니다. 끝점은 Kerberos만을 사용하는 Windows 인증을 사용하도록 구성됩니다. `ENCRYPTION` 옵션은 암호화되거나 암호화되지 않은 데이터를 모두 지원하기 위해 기본값이 아닌 `SUPPORTED`로 구성됩니다. 끝점은 파트너와 미러링 모니터 역할을 모두 지원하도록 구성됩니다.  
  
```  
CREATE ENDPOINT endpoint_mirroring  
    STATE = STARTED  
    AS TCP ( LISTENER_PORT = 7022 )  
    FOR DATABASE_MIRRORING (  
       AUTHENTICATION = WINDOWS KERBEROS,  
       ENCRYPTION = SUPPORTED,  
       ROLE=ALL);  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [암호화 알고리즘 선택](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [DROP ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/drop-endpoint-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

