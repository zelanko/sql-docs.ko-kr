---
title: ALTER ENDPOINT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER ENDPOINT
- ALTER_ENDPOINT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER ENDPOINT statement
- modifying endpoints
- endpoints [SQL Server], modifying
ms.assetid: 70f35566-30cf-47c6-8394-dfe5d71629d3
caps.latest.revision: 56
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 972788ef2369c8b885e9c736b2b2e71ebc89470c
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38052961"
---
# <a name="alter-endpoint-transact-sql"></a>ALTER ENDPOINT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  다음 방법으로 기존 끝점을 수정할 수 있도록 합니다.  
  
-   기존 끝점에 새 메서드 추가  
  
-   끝점의 기존 메서드 수정 또는 삭제  
  
-   끝점 속성 변경  
  
> [!NOTE]  
>  이 항목에서는 ALTER ENDPOINT의 구문과 인수에 대해 설명합니다. CREATE ENDPOINT와 ALTER ENDPOINT의 공통 인수에 대한 설명은 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)를 참조하십시오.  
  
 네이티브 XML 웹 서비스(SOAP/HTTP 끝점)는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터는 더 이상 사용되지 않습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
ALTER ENDPOINT endPointName [ AUTHORIZATION login ]  
[ STATE = { STARTED | STOPPED | DISABLED } ]  
[ AS { TCP } ( <protocol_specific_items> ) ]  
[ FOR { TSQL | SERVICE_BROKER | DATABASE_MIRRORING } (  
   <language_specific_items>  
        ) ]  
  
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
   [ , ENCRYPTION = { DISABLED   
       |   
         {{SUPPORTED | REQUIRED }   
       [ ALGORITHM { RC4 | AES | AES RC4 | RC4 AES } ] }   
   ]  
  
  [ , MESSAGE_FORWARDING = {ENABLED | DISABLED} ]  
  [ , MESSAGE_FORWARD_SIZE = forwardSize  
)  
  
<FOR DATABASE_MIRRORING_language_specific_arguments> ::=  
FOR DATABASE_MIRRORING (  
   [ AUTHENTICATION = {   
      WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]  
      | CERTIFICATE certificate_name   
      | WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ] CERTIFICATE certificate_name   
      | CERTIFICATE certificate_name WINDOWS [ { NTLM | KERBEROS | NEGOTIATE } ]   
    } ]  
   [ , ENCRYPTION = { DISABLED   
       |   
         {{SUPPORTED | REQUIRED }   
       [ ALGORITHM { RC4 | AES | AES RC4 | RC4 AES } ] }   
    ]   
   [ , ] ROLE = { WITNESS | PARTNER | ALL }  
)  
  
```  
  
## <a name="arguments"></a>인수  
  
> [!NOTE]  
>  다음은 ALTER ENDPOINT 관련 인수입니다. 나머지 인수에 대한 설명은 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)를 참조하십시오.  
  
 **AS** { **TCP** }  
 **ALTER ENDPOINT**를 사용하여 전송 프로프콜은 변경할 수 없습니다.  
  
 **AUTHORIZATION** *로그인*  
 **AUTHORIZATION** 옵션은 **ALTER ENDPOINT**에서 사용할 수 없습니다. 소유권은 끝점이 생성된 경우에만 할당될 수 있습니다.  
  
 **FOR** { **TSQL** | **SERVICE_BROKER** | **DATABASE_MIRRORING** }  
 **ALTER ENDPOINT**를 사용하여 페이로드 유형은 변경할 수 없습니다.  
  
## <a name="remarks"></a>Remarks  
 ALTER ENDPOINT를 사용할 때는 업데이트할 매개 변수만 지정합니다. 기존 끝점의 모든 속성은 명시적으로 변경하지 않는 한 동일하게 유지됩니다.  
  
 사용자 트랜잭션 내에서 ENDPOINT DDL 문을 실행할 수 없습니다.  
  
 끝점에 사용할 암호화 알고리즘을 선택하는 방법은 [암호화 알고리즘 선택](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)을 참조하십시오.  
  
> [!NOTE]  
>  RC4 알고리즘은 이전 버전과의 호환성을 위해서만 지원됩니다. 데이터베이스의 호환성 수준이 90 또는 100인 경우 새 자료는 RC4 또는 RC4_128로만 암호화할 수 있습니다. 이 옵션은 사용하지 않는 것이 좋습니다. 대신 AES 알고리즘 중 하나와 같은 새 알고리즘을 사용하십시오. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상 버전에서 RC4 또는 RC4_128을 사용하여 암호화된 자료는 모든 호환성 수준에서 해독할 수 있습니다.  
>   
>  RC4는 비교적 약한 알고리즘이고 AES는 비교적 강력한 알고리즘입니다. 그러나 AES는 RC4보다 속도가 훨씬 느립니다. 속도보다 보안의 우선 순위가 높은 경우 AES를 사용하는 것이 좋습니다.  
  
## <a name="permissions"></a>Permissions  
 사용자는 **sysadmin** 고정 서버 역할의 멤버 또는 끝점 소유자이거나 ALTER ANY ENDPOINT 권한을 부여받아야 합니다.  
  
 기존 끝점의 소유권을 변경하려면 ALTER AUTHORIZATION 문을 사용해야 합니다. 자세한 내용은 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)을 참조하세요.  
  
 자세한 내용은 [GRANT 끝점 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [DROP ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/drop-endpoint-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
