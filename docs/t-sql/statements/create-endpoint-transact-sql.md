---
title: CREATE ENDPOINT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ENDPOINT
- CREATE ENDPOINT
- ENDPOINT_TSQL
- CREATE_ENDPOINT_TSQL
dev_langs:
- TSQL
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: fc582f9328196233768e1fd7e7bd2bb81688c81d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66413445"
---
# <a name="create-endpoint-transact-sql"></a>CREATE ENDPOINT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  클라이언트 응용 프로그램에 사용할 수 있는 메서드를 포함하여 엔드포인트를 만들고 속성을 정의합니다. 관련 사용 권한에 대한 자세한 내용은 [GRANT 엔드포인트 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)을 참조하세요.  
  
 CREATE ENDPOINT의 구문은 논리적으로 다음과 같이 두 부분으로 나눌 수 있습니다.  
  
-   첫 번째 부분은 AS로 시작하고 FOR 절 앞에서 끝납니다.  
  
     이 부분에서는 전송 프로토콜(TCP)과 관련된 정보를 제공하며 엔드포인트의 수신 포트 번호를 설정하고 엔드포인트 인증 방법 및/또는 엔드포인트에 대한 액세스를 차단할 IP 주소(있는 경우) 목록을 설정합니다.  
  
-   두 번째 부분은 FOR 절로 시작합니다.  
  
     이 부분에서는 엔드포인트에서 지원되는 페이로드를 정의합니다. 지원되는 페이로드 유형인 [!INCLUDE[tsql](../../includes/tsql-md.md)], Service Broker, 데이터베이스 미러링 중에서 하나를 정의할 수 있습니다. 또한 이 부분에는 언어별 정보도 포함됩니다.  
  
> **참고:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서는 네이티브 XML 웹 서비스(SOAP/HTTP 엔드포인트)가 제거되었습니다.  
  
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
  [ [ , ] LISTENER_IP = ALL | ( xx.xx.xx.xx IPv4 address ) | ( '__:__1' IPv6 address ) ]  
  
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
 만들어지는 엔드포인트에 할당할 이름입니다. 엔드포인트를 업데이트하거나 삭제할 때 사용합니다.  
  
 AUTHORIZATION *로그인*  
 새로 만들어지는 엔드포인트 개체의 소유권을 할당할 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Windows 로그인을 지정합니다. AUTHORIZATION이 지정되지 않은 경우 기본적으로 호출자가 새로 만들어지는 개체의 소유자가 됩니다.  
  
 AUTHORIZATION을 지정하여 소유권을 할당하려면 호출자는 지정된 *login*에 대해 IMPERSONATE 권한이 있어야 합니다.  
  
 소유권을 다시 할당하려면 [ALTER ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)를 참조하세요.  
  
 STATE **=** { STARTED | **STOPPED** | DISABLED }  
 엔드포인트가 생성될 때의 엔드포인트 상태입니다. 엔드포인트를 만들 때 상태를 지정하지 않으면 STOPPED가 기본값이 됩니다.  
  
 STARTED  
 엔드포인트가 시작되어 연결 수신 대기 중입니다.  
  
 DISABLED  
 엔드포인트가 해제되었습니다. 이 상태일 경우 서버는 포트 요청을 수신하지만 오류를 클라이언트에 반환합니다.  
  
 **STOPPED**  
 엔드포인트가 중지되었습니다. 이 상태에서 서버는 엔드포인트 포트로의 수신을 대기하거나 엔드포인트를 사용하기 위해 시도된 요청에 응답하지 않습니다.  
  
 상태를 변경하려면 [ALTER ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)를 사용하세요.  
  
 AS { TCP }  
 사용할 전송 프로토콜을 지정합니다.  
  
 FOR { TSQL | SERVICE_BROKER | DATABASE_MIRRORING }  
 페이로드 유형을 지정합니다.  
  
 현재 `<language_specific_arguments>` 매개 변수에 전달할 [!INCLUDE[tsql](../../includes/tsql-md.md)] 언어 관련 인수는 없습니다.  
  
 **TCP 프로토콜 옵션**  
  
 다음 인수는 TCP 프로토콜 옵션에만 적용됩니다.  
  
 LISTENER_PORT **=** _listenerPort_  
 Service Broker TCP/IP 프로토콜을 통한 연결을 수신하는 포트 번호를 지정합니다. 규칙에 따라 4022가 사용되지만 1024와 32767 사이의 모든 번호를 사용할 수 있습니다.  
  
 LISTENER_IP **=** ALL | **(** _4-part-ip_ **)**  |  **(** "*ip_address_v6*" **)**  
 엔드포인트가 수신하는 IP 주소를 지정합니다. 기본값은 ALL입니다. 이는 수신기가 모든 유효한 IP 주소에 대한 연결을 허용함을 의미합니다.  
  
 정규화된 도메인 이름(`ALTER DATABASE SET PARTNER = partner_IP_address` 또는 `ALTER DATABASE SET WITNESS = witness_IP_address`) 대신 IP 주소를 사용하여 데이터베이스 미러링을 구성하는 경우 미러링 엔드포인트를 만들 때 `LISTENER_IP =IP_address` 대신 `LISTENER_IP=ALL`를 지정해야 합니다.  
  
 **SERVICE_BROKER and DATABASE_MIRRORING 옵션**  
  
 다음 AUTHENTICATION 및 ENCRYPTION 인수는 SERVICE_BROKER 및 DATABASE_MIRRORING 옵션에 사용할 수 있는 공통 인수입니다.  
  
> [!NOTE]  
>  SERVICE_BROKER와 관련된 옵션은 이 섹션 뒷부분의 "SERVICE_BROKER 옵션"을 참조하십시오. DATABASE_MIRRORING과 관련된 옵션은 이 섹션 뒷부분의 "DATABASE_MIRRORING 옵션"을 참조하십시오.  
  
 AUTHENTICATION **=** \<authentication_options> 이 엔드포인트에 대한 연결의 TCP/IP 인증 요구 사항을 지정합니다. 기본값은 WINDOWS입니다.  
  
 지원되는 인증 방법에는 NTLM 또는 Kerberos가 있으며 둘 다 사용할 수도 있습니다.  
  
> [!IMPORTANT]  
>  서버 인스턴스의 모든 미러링 연결은 하나의 데이터베이스 미러링 엔드포인트를 사용합니다. 추가 데이터베이스 미러링 엔드포인트를 만들려고 시도하면 실패합니다.  
  
 **\<authentication_options> ::=**  
  
 **WINDOWS** [ { NTLM | KERBEROS | **NEGOTIATE** } ]  
 엔드포인트가 인증을 위해 Windows 인증 프로토콜을 사용하여 연결하도록 지정합니다. 기본값입니다.  
  
 인증 방법(NTLM 또는 KERBEROS)을 지정한 경우 항상 해당 방법이 인증 프로토콜로 사용됩니다. 기본값인 NEGOTIATE를 적용하면 엔드포인트가 Windows 협상 프로토콜을 사용하여 NTLM이나 Kerberos를 선택합니다.  
  
 CERTIFICATE *certificate_name*  
 엔드포인트가 *certificate_name*에 지정된 인증서를 사용하여 인증용 ID를 설정하고 연결을 인증하도록 지정합니다. 먼 엔드포인트에는 지정된 인증서의 프라이빗 키와 일치하는 퍼블릭 키를 가진 인증서가 있어야 합니다.  
  
 WINDOWS [ { NTLM | KERBEROS | **NEGOTIATE** } ] CERTIFICATE *certificate_name*  
 Windows 인증을 사용하여 엔드포인트가 연결을 시도하고 이 시도가 실패하면 지정한 인증서를 사용하여 연결을 시도하도록 지정합니다.  
  
 CERTIFICATE *certificate_name* WINDOWS [ { NTLM | KERBEROS | **NEGOTIATE** } ]  
 지정한 인증서를 사용하여 엔드포인트가 연결을 시도하고 이 시도가 실패하면 Windows 인증을 사용하여 연결을 시도하도록 지정합니다.  
  
 ENCRYPTION = { DISABLED | SUPPORTED | **REQUIRED** } [ALGORITHM { **AES** | RC4 | AES RC4 | RC4 AES } ]  
 프로세스에서 암호화를 사용할지 여부를 지정합니다. 기본값은 REQUIRED입니다.  
  
 DISABLED  
 연결을 통해 전송되는 데이터를 암호화하지 않도록 지정합니다.  
  
 SUPPORTED  
 반대쪽 엔드포인트가 SUPPORTED나 REQUIRED로 지정된 경우에만 데이터를 암호화하도록 지정합니다.  
  
 REQUIRED  
 이 엔드포인트에 대한 연결이 암호화를 사용하도록 지정합니다. 따라서 이 엔드포인트에 연결하려면 다른 엔드포인트의 ENCRYPTION이 SUPPORTED 또는 REQUIRED로 설정되어 있어야 합니다.  
  
 필요에 따라 다음과 같이 ALGORITHM 인수를 사용하여 엔드포인트에 사용되는 암호화 형식을 지정할 수 있습니다.  
  
 **AES**  
 엔드포인트가 반드시 AES 알고리즘을 반드시 사용하도록 지정합니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상에서 기본값입니다.  
  
 RC4  
 엔드포인트가 반드시 RC4 알고리즘을 사용하도록 지정합니다. [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]까지 기본값입니다.  
  
> [!NOTE]  
>  RC4 알고리즘은 이전 버전과의 호환성을 위해서만 지원됩니다. 데이터베이스의 호환성 수준이 90 또는 100인 경우 새 자료는 RC4 또는 RC4_128로만 암호화할 수 있습니다. 이 옵션은 사용하지 않는 것이 좋습니다. 대신 AES 알고리즘 중 하나와 같은 새 알고리즘을 사용하십시오. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상 버전에서 RC4 또는 RC4_128을 사용하여 암호화된 자료는 모든 호환성 수준에서 해독할 수 있습니다.  
  
 AES RC4  
 두 엔드포인트가 암호화 알고리즘에 대해 협상하고 이 엔드포인트가 AES 알고리즘에 우선권을 주도록 지정합니다.  
  
 RC4 AES  
 두 엔드포인트가 암호화 알고리즘에 대해 협상하고 이 엔드포인트가 RC4 알고리즘에 우선권을 주도록 지정합니다.  
  
> [!NOTE]  
>  RC4 알고리즘은 더 이상 사용되지 않습니다. [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] AES를 사용하는 것이 좋습니다.  
  
 양쪽 엔드포인트가 두 알고리즘을 모두 지정하지만 순서가 다른 경우 연결을 수락하는 엔드포인트의 알고리즘이 적용됩니다.  
  
 **SERVICE_BROKER 옵션**  
  
 다음은 SERVICE_BROKER 옵션에 대한 인수입니다.  
  
 MESSAGE_FORWARDING **=** { ENABLED | **DISABLED** }  
 엔드포인트에서 수신한 메시지가 다른 위치에 있는 서비스에 관련된 것일 경우 이 메시지를 전달할지 여부를 결정합니다.  
  
 ENABLED  
 전달 주소가 있을 경우 메시지를 전달합니다.  
  
 DISABLED  
 다른 위치에 있는 서비스에 대한 메시지를 무시합니다. 기본값입니다.  
  
 MESSAGE_FORWARD_SIZE **=** _forward_size_  
 엔드포인트가 전달할 메시지를 저장할 때 사용할 수 있는 최대 저장 크기(MB)를 지정합니다.  
  
 **DATABASE_MIRRORING 옵션**  
  
 다음은 DATABASE_MIRRORING 옵션에 대한 인수입니다.  
  
 ROLE **=** { WITNESS | PARTNER | ALL }  
 데이터베이스 미러링 역할 또는 엔드포인트가 지원하는 역할을 지정합니다.  
  
 WITNESS  
 미러링 프로세스에서 엔드포인트가 미러링 모니터의 역할을 수행하도록 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)]의 경우 WITNESS 옵션만 사용할 수 있습니다.  
  
 PARTNER  
 미러링 프로세스에서 엔드포인트가 파트너의 역할을 수행하도록 합니다.  
  
 ALL  
 미러링 프로세스에서 엔드포인트가 미러링 모니터 및 파트너 역할을 모두 수행하도록 지정합니다.  
  
 이러한 역할에 대한 자세한 내용은 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)을 참조하세요.  
  
> [!NOTE]  
>  DATABASE_MIRRORING에 대한 기본 포트는 없습니다.  
  
## <a name="remarks"></a>Remarks  
 ENDPOINT DDL 문은 사용자 트랜잭션 내에서 실행할 수 없습니다. 활성 스냅샷 격리 수준 트랜잭션이 변경되는 엔드포인트를 사용하는 경우에도 ENDPOINT DDL 문은 실패하지 않습니다.  
  
 ENDPOINT에 대한 요청을 실행할 수 있는 사람은 다음과 같습니다.  
  
-   **sysadmin** 고정 서버 역할의 멤버  
  
-   엔드포인트의 소유자  
  
-   엔드포인트에 대한 CONNECT 권한이 부여된 사용자 또는 그룹  
  
## <a name="permissions"></a>사용 권한  
 CREATE ENDPOINT 권한 또는 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다. 자세한 내용은 [GRANT 엔드포인트 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)을 참조하세요.  
  
## <a name="example"></a>예제  
  
### <a name="creating-a-database-mirroring-endpoint"></a>데이터베이스 미러링 엔드포인트 만들기  
 다음 예에서는 데이터베이스 미러링 엔드포인트를 만듭니다. 사용할 수 있는 포트 번호라면 어떤 것이라도 관계 없으나 여기서는 엔드포인트가 `7022` 포트 번호를 사용합니다. 엔드포인트는 Kerberos만을 사용하는 Windows 인증을 사용하도록 구성됩니다. `ENCRYPTION` 옵션은 암호화되거나 암호화되지 않은 데이터를 모두 지원하기 위해 기본값이 아닌 `SUPPORTED`로 구성됩니다. 엔드포인트는 파트너와 미러링 모니터 역할을 모두 지원하도록 구성됩니다.  
  
```sql  
CREATE ENDPOINT endpoint_mirroring  
    STATE = STARTED  
    AS TCP ( LISTENER_PORT = 7022 )  
    FOR DATABASE_MIRRORING (  
       AUTHENTICATION = WINDOWS KERBEROS,  
       ENCRYPTION = SUPPORTED,  
       ROLE=ALL);  
GO  
```  

### <a name="create-a-new-endpoint-pointing-to-a-specific-ipv4-address-and-port"></a>특정 IPv4 주소 및 포트를 가리키는 새 엔드포인트 만들기

```sql
CREATE ENDPOINT ipv4_endpoint_special
STATE = STARTED
AS TCP (
    LISTENER_PORT = 55555, LISTENER_IP = (10.0.75.1)
)
FOR TSQL ();

GRANT CONNECT ON ENDPOINT::[TSQL Default TCP] TO public; -- Keep existing public permission on default endpoint for demo purpose
GRANT CONNECT ON ENDPOINT::ipv4_endpoint_special
TO login_name;
```

### <a name="create-a-new-endpoint-pointing-to-a-specific-ipv6-address-and-port"></a>특정 IPv6 주소 및 포트를 가리키는 새 엔드포인트 만들기

```sql
CREATE ENDPOINT ipv6_endpoint_special
STATE = STARTED
AS TCP (
    LISTENER_PORT = 55555, LISTENER_IP = ('::1')
)
FOR TSQL ();

GRANT CONNECT ON ENDPOINT::[TSQL Default TCP] TO public;
GRANT CONNECT ON ENDPOINT::ipv6_endpoint_special

```
  
## <a name="see-also"></a>관련 항목:  
 [ALTER ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [암호화 알고리즘 선택](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [DROP ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/drop-endpoint-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

