---
title: Audit Broker Login 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Audit Broker Login event class
ms.assetid: af9b1153-2791-40ef-a95c-50923cd0cc97
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: b532bf4cdc9f65fea1b988b13f865c1437e94c8a
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39546823"
---
# <a name="audit-broker-login-event-class"></a>Audit Broker Login 이벤트 클래스
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 **Audit Broker Login** 이벤트를 만들어 Service Broker 전송 보안과 관련된 감사 메시지를 보고합니다.  
  
## <a name="audit-broker-login-event-class-data-columns"></a>Audit Broker Login 이벤트 클래스 데이터 열  
  
|데이터 열|형식|설명|열 번호|필터 가능|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|이 이벤트 클래스에서는 사용되지 않습니다.|10|사용자 계정 컨트롤|  
|**ClientProcessID**|**int**|이 이벤트 클래스에서는 사용되지 않습니다.|9|사용자 계정 컨트롤|  
|**DatabaseID**|**int**|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|사용자 계정 컨트롤|  
|**EventClass**|**int**|캡처된 이벤트 클래스 유형입니다. **Audit Broker Login** 에 대해서는 항상 **159**입니다.|27|아니오|  
|**EventSequence**|**int**|이 이벤트의 시퀀스 번호입니다.|51|아니오|  
|**EventSubClass**|**int**|각 이벤트 클래스에 대한 자세한 정보를 제공하는 이벤트 하위 클래스 유형입니다. 다음 표에서는 이 이벤트에 대한 이벤트 하위 클래스 값을 나열합니다.|21|사용자 계정 컨트롤|  
|**FileName**|**nvarchar**|원격 Broker 인증 수준입니다. 원격 Broker 끝점에서 구성된 지원되는 인증 방법입니다. 둘 이상의 메서드를 사용할 수 있는 경우 수락하는(대상) 끝점에서 먼저 시도할 메서드를 결정합니다. 가능한 값은<br /><br /> **없음**. 인증 방법이 구성되어 있지 않습니다.<br /><br /> **NTLM**. NTLM 인증이 필요합니다.<br /><br /> **KERBEROS**- Kerberos 인증이 필요합니다.<br /><br /> **NEGOTIATE**- Windows에서 인증 방법을 협상합니다.<br /><br /> **CERTIFICATE**- 끝점에 대해 구성된 인증서가 필요합니다. 이 인증서는 **master** 데이터베이스에 저장되어 있습니다.<br /><br /> **NTLM, CERTIFICATE**- NTLM 또는 SSL 인증서 인증을 적용합니다.<br /><br /> **KERBEROS, CERTIFICATE**- Kerberos 또는 끝점 인증서 인증을 적용합니다.<br /><br /> **NEGOTIATE, CERTIFICATE**- Windows에서 인증 방법을 협상하거나 끝점 인증서 인증을 사용합니다.<br /><br /> **CERTIFICATE, NTLM**- 끝점 인증서 또는 NTLM 인증을 적용합니다.<br /><br /> **CERTIFICATE, KERBEROS**- 끝점 인증서 또는 Kerberos 인증을 적용합니다.<br /><br /> **CERTIFICATE, NEGOTIATE**- 끝점 인증서 인증을 적용하거나 Windows에서 인증 방법을 협상합니다.|36|아니오|  
|**HostName**|**nvarchar**|이 이벤트 클래스에서는 사용되지 않습니다.|8|사용자 계정 컨트롤|  
|**IsSystem**|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|아니오|  
|**LoginSid**|**image**|로그인한 사용자의 SID(보안 ID)입니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|사용자 계정 컨트롤|  
|**NTDomainName**|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|사용자 계정 컨트롤|  
|**NTUserName**|**nvarchar**|이 이벤트를 생성한 연결을 소유하고 있는 사용자의 이름입니다.|6|사용자 계정 컨트롤|  
|**ObjectName**|**nvarchar**|이 연결에 사용된 연결 문자열입니다.|34|아니오|  
|**OwnerName**|**nvarchar**|로컬 Broker 끝점에서 구성된 지원되는 인증 방법입니다. 둘 이상의 메서드를 사용할 수 있는 경우 수락하는(대상) 끝점에서 먼저 시도할 메서드를 결정합니다. 가능한 값은<br /><br /> **없음**. 인증 방법이 구성되어 있지 않습니다.<br /><br /> **NTLM**. NTLM 인증이 필요합니다.<br /><br /> **KERBEROS**- Kerberos 인증이 필요합니다.<br /><br /> **NEGOTIATE**- Windows에서 인증 방법을 협상합니다.<br /><br /> **CERTIFICATE**- 끝점에 대해 구성된 인증서가 필요합니다. 이 인증서는 **master** 데이터베이스에 저장되어 있습니다.<br /><br /> **NTLM, CERTIFICATE**- NTLM 또는 SSL 인증서 인증을 적용합니다.<br /><br /> **KERBEROS, CERTIFICATE**- Kerberos 또는 끝점 인증서 인증을 적용합니다.<br /><br /> **NEGOTIATE, CERTIFICATE**- Windows에서 인증 방법을 협상하거나 끝점 인증서 인증을 사용합니다.<br /><br /> **CERTIFICATE, NTLM**- 끝점 인증서 또는 NTLM 인증을 적용합니다.<br /><br /> **CERTIFICATE, KERBEROS**- 끝점 인증서 또는 Kerberos 인증을 적용합니다.<br /><br /> **CERTIFICATE, NEGOTIATE**- 끝점 인증서 인증을 적용하거나 Windows에서 인증 방법을 협상합니다.|37|아니오|  
|**ProviderName**|**nvarchar**|이 연결에 사용된 인증 방법입니다.|46|아니오|  
|**RoleName**|**nvarchar**|연결의 역할입니다. 이 역할은 **시작자** 또는 **대상**입니다.|38|아니오|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|**nvarchar**|추적 중인 SQL Server 인스턴스의 이름입니다.|26|아니오|  
|**SPID**|**int**|SQL Server가 클라이언트와 관련된 프로세스에 할당한 서버 프로세스 ID입니다.|12|사용자 계정 컨트롤|  
|**StartTime**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|사용자 계정 컨트롤|  
|**State**|**int**|SQL Server 원본 코드 내에서 이벤트가 생성된 위치를 나타냅니다. 이 이벤트가 생성될 수 있는 각 위치의 상태 코드는 서로 다릅니다. Microsoft 지원 엔지니어는 이 상태 코드를 사용하여 이벤트가 생성된 위치를 찾을 수 있습니다.|30|아니오|  
|**TargetUserName**|**nvarchar**|로그인 상태입니다. 다음 중 하나입니다.<br /><br /> INITIAL<br /><br /> WAIT LOGIN NEGOTIATE<br /><br /> ONE ISC<br /><br /> ONE ASC<br /><br /> TWO ISC<br /><br /> TWO ASC<br /><br /> WAIT ISC Confirm<br /><br /> WAIT ASC Confirm<br /><br /> WAIT REJECT<br /><br /> WAIT PRE-MASTER SECRET<br /><br /> WAIT VALIDATION<br /><br /> WAIT ARBITRATION<br /><br /> ONLINE<br /><br /> error<br /><br /> <br /><br /> **참고**: ISC = 보안 컨텍스트 시작. ASC = 보안 컨텍스트 허용|39|아니오|  
|**TransactionID**|**bigint**|시스템이 할당한 트랜잭션 ID입니다.|4|아니오|  
  
 다음 표에서는 이 이벤트 클래스에 대한 하위 클래스 값을 나열합니다.  
  
|ID|하위 클래스|설명|  
|--------|--------------|-----------------|  
|@shouldalert|Login Success|Login Success 이벤트는 인접한 Broker 로그인 프로세스가 성공적으로 끝났음을 보고합니다.|  
|2|Login Protocol Error|Login Protocol Error 이벤트는 Broker가 올바른 형식이지만 로그인 프로세스의 현재 상태에 맞지 않는 메시지를 수신했음을 보고합니다. 메시지가 잘못 전송되었거나 순서에 맞지 않게 전송되었을 수 있습니다.|  
|3|Message Format Error|Message Format Error 이벤트는 Broker가 해당 형식에 맞지 않는 메시지를 수신했음을 보고합니다. 메시지가 손상되었거나 SQL Server가 아닌 프로그램에서 Service Broker가 사용하는 포트로 메시지를 보내는 것일 수 있습니다.|  
|4|Negotiate Failure|Negotiate Failure 이벤트는 로컬 Broker와 원격 Broker가 상호 배타적인 인증 수준을 지원하고 있음을 보고합니다.|  
|5|Authentication Failure|Authentication Failure 이벤트는 Service Broker가 오류로 인해 연결을 인증할 수 없음을 보고합니다. Windows 인증일 경우 이 이벤트는 Service Broker가 Windows 인증을 사용할 수 없음을 보고합니다. 인증서 기반 인증일 경우 이 이벤트는 Service Broker가 인증서에 액세스할 수 없음을 보고합니다.|  
|6|Authorization Failure|Authorization Failure 이벤트는 Service Broker에서 연결 인증을 거부했음을 보고합니다. Windows 인증일 경우 이 이벤트는 연결의 보안 식별자가 데이터베이스 사용자와 일치하지 않음을 보고합니다. 인증서 기반 인증일 경우 이 이벤트는 메시지에 전달된 공용 키가 데이터베이스의 인증서와 맞지 않음을 보고합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [CREATE ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [ALTER ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
