---
description: Audit Database Mirroring Login 이벤트 클래스
title: Audit Database Mirroring Login 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], database mirroring
- Audit Database Mirroring Login event class
- database mirroring [SQL Server], event notifications
ms.assetid: d0bd436d-aade-4208-a7e5-75cf3b5d0ce9
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ddab7518314b15b3a74875f8ce6a22b9e752322a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97476484"
---
# <a name="audit-database-mirroring-login-event-class"></a>Audit Database Mirroring Login 이벤트 클래스
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 **Audit Database Mirroring Login** 이벤트를 만들어 데이터베이스 미러링 전송 보안과 관련된 감사 메시지를 보고합니다.  
  
## <a name="audit-database-mirroring-login-event-class-data-columns"></a>Audit Database Mirroring Login 이벤트 클래스 데이터 열  
  
|데이터 열|Type|Description|열 번호|필터 가능|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|이 이벤트 클래스에서는 사용되지 않습니다.|10|예|  
|**ClientProcessID**|**int**|이 이벤트 클래스에서는 사용되지 않습니다.|9|예|  
|**DatabaseID**|**int**|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|**EventClass**|**int**|캡처된 이벤트 클래스 유형입니다. **Audit Database Mirroring Login** 에 대해서는 항상 **154** 입니다.|27|예|  
|**EventSequence**|**int**|이 이벤트의 시퀀스 번호입니다.|51|예|  
|**EventSubClass**|**int**|각 이벤트 클래스에 대한 자세한 정보를 제공하는 이벤트 하위 클래스 유형입니다. 다음 표에서는 이 이벤트에 대한 이벤트 하위 클래스 값을 나열합니다.|21|예|  
|**FileName**|**nvarchar**|원격 데이터베이스 미러링 엔드포인트에서 구성된 지원되는 인증 방법입니다. 둘 이상의 메서드를 사용할 수 있는 경우 수락하는(대상) 엔드포인트에서 먼저 시도할 메서드를 결정합니다. 가능한 값은 다음과 같습니다.<br /><br /> <br /><br /> **없음**. 인증 방법이 구성되어 있지 않습니다.<br /><br /> **NTLM**. NTLM 인증이 필요합니다.<br /><br /> **KERBEROS**- Kerberos 인증이 필요합니다.<br /><br /> **NEGOTIATE**- Windows에서 인증 방법을 협상합니다.<br /><br /> **CERTIFICATE**- 엔드포인트에 대해 구성된 인증서가 필요합니다. 이 인증서는 **master** 데이터베이스에 저장되어 있습니다.<br /><br /> **NTLM, CERTIFICATE**- NTLM 또는 엔드포인트 인증서 인증을 적용합니다.<br /><br /> **KERBEROS, CERTIFICATE**- Kerberos 또는 엔드포인트 인증서 인증을 적용합니다.<br /><br /> **NEGOTIATE, CERTIFICATE**- Windows에서 인증 방법을 협상하거나 엔드포인트 인증서 인증을 사용합니다.<br /><br /> **CERTIFICATE, NTLM**- 엔드포인트 인증서 또는 NTLM 인증을 적용합니다.<br /><br /> **CERTIFICATE, KERBEROS**- 엔드포인트 인증서 또는 Kerberos 인증을 적용합니다.<br /><br /> **CERTIFICATE, NEGOTIATE**- 엔드포인트 인증서 인증을 적용하거나 Windows에서 인증 방법을 협상합니다.|36|예|  
|**HostName**|**nvarchar**|이 이벤트 클래스에서는 사용되지 않습니다.|8|예|  
|**IsSystem**|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|**LoginSid**|**image**|로그인한 사용자의 SID(보안 ID)입니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|**NTDomainName**|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|**NTUserName**|**nvarchar**|이 이벤트를 생성한 연결을 소유하고 있는 사용자의 이름입니다.|6|예|  
|**ObjectName**|**nvarchar**|이 연결에 사용된 연결 문자열입니다.|34|예|  
|**OwnerName**|**nvarchar**|로컬 데이터베이스 미러링 엔드포인트에서 구성된 지원되는 인증 방법입니다. 둘 이상의 메서드를 사용할 수 있는 경우 수락하는(대상) 엔드포인트에서 먼저 시도할 메서드를 결정합니다. 가능한 값은 다음과 같습니다.<br /><br /> <br /><br /> **없음**. 인증 방법이 구성되어 있지 않습니다.<br /><br /> **NTLM**. NTLM 인증이 필요합니다.<br /><br /> **KERBEROS**- Kerberos 인증이 필요합니다.<br /><br /> **NEGOTIATE**- Windows에서 인증 방법을 협상합니다.<br /><br /> **CERTIFICATE**- 엔드포인트에 대해 구성된 인증서가 필요합니다. 이 인증서는 **master** 데이터베이스에 저장되어 있습니다.<br /><br /> **NTLM, CERTIFICATE**- NTLM 또는 엔드포인트 인증서 인증을 적용합니다.<br /><br /> **KERBEROS, CERTIFICATE**- Kerberos 또는 엔드포인트 인증서 인증을 적용합니다.<br /><br /> **NEGOTIATE, CERTIFICATE**- Windows에서 인증 방법을 협상하거나 엔드포인트 인증서 인증을 사용합니다.<br /><br /> **CERTIFICATE, NTLM**- 엔드포인트 인증서 또는 NTLM 인증을 적용합니다.<br /><br /> **CERTIFICATE, KERBEROS**- 엔드포인트 인증서 또는 Kerberos 인증을 적용합니다.<br /><br /> **CERTIFICATE, NEGOTIATE**- 엔드포인트 인증서 인증을 적용하거나 Windows에서 인증 방법을 협상합니다.|37|예|  
|**ProviderName**|**nvarchar**|이 연결에 사용된 인증 방법입니다.|46|예|  
|**RoleName**|**nvarchar**|연결의 역할입니다. 이 역할은 **시작자** 또는 **대상** 입니다.|38|예|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|예|  
|**SPID**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 클라이언트와 관련된 프로세스에 할당한 서버 프로세스 ID입니다.|12|예|  
|**StartTime**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|**State**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원본 코드 내에서 이벤트가 생성된 위치를 나타냅니다. 이 이벤트가 생성될 수 있는 각 위치의 상태 코드는 서로 다릅니다. Microsoft 지원 엔지니어는 이 상태 코드를 사용하여 이벤트가 생성된 위치를 찾을 수 있습니다.|30|예|  
|**TargetUserName**|**nvarchar**|로그인 상태입니다. 다음 중 하나:<br /><br /> **INITIAL**<br /><br /> **WAIT LOGIN NEGOTIATE**<br /><br /> **ONE ISC**<br /><br /> **ONE ASC**<br /><br /> **TWO ISC**<br /><br /> **TWO ASC**<br /><br /> **WAIT ISC Confirm**<br /><br /> **WAIT ASC Confirm**<br /><br /> **WAIT REJECT**<br /><br /> **WAIT PRE-MASTER SECRET**<br /><br /> **WAIT VALIDATION**<br /><br /> **WAIT ARBITRATION**<br /><br /> **ONLINE**<br /><br /> **ERROR**<br /><br /> <br /><br /> 참고: ISC = 보안 컨텍스트 시작. ASC = 보안 컨텍스트 허용.|39|예|  
|**TransactionID**|**bigint**|시스템이 할당한 트랜잭션 ID입니다.|4|예|  
  
 다음 표에서는 이 이벤트 클래스에 대한 하위 클래스 값을 나열합니다.  
  
|ID|하위 클래스|Description|  
|--------|--------------|-----------------|  
|1|Login Success|Login Success 이벤트는 인접한 데이터베이스 미러링 로그인 프로세스가 성공적으로 끝났음을 보고합니다.|  
|2|Login Protocol Error|Login Protocol Error 이벤트는 데이터베이스 미러링 로그인이 올바른 형식이지만 로그인 프로세스의 현재 상태에 맞지 않는 메시지를 수신했음을 보고합니다. 메시지가 잘못 전송되었거나 순서에 맞지 않게 전송되었을 수 있습니다.|  
|3|Message Format Error|Message Format Error 이벤트는 데이터베이스 미러링 로그인이 예상 형식에 맞지 않는 메시지를 수신했음을 보고합니다. 메시지가 손상되었거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 아닌 프로그램에서 데이터베이스 미러링이 사용하는 포트로 메시지를 보내는 것일 수 있습니다.|  
|4|Negotiate Failure|Negotiate Failure 이벤트는 로컬 데이터베이스 미러링 엔드포인트와 원격 데이터베이스 미러링 엔드포인트가 상호 배타적인 인증 수준을 지원하고 있음을 보고합니다.|  
|5|Authentication Failure|Authentication Failure 이벤트는 데이터베이스 미러링 엔드포인트가 오류로 인해 연결을 인증할 수 없음을 보고합니다. Windows 인증일 경우 이 이벤트는 데이터베이스 미러링 엔드포인트가 Windows 인증을 사용할 수 없음을 보고합니다. 인증서 기반 인증일 경우 이 이벤트는 데이터베이스 미러링 엔드포인트가 인증서에 액세스할 수 없음을 보고합니다.|  
|6|권한 부여 실패|Authorization Failure 이벤트는 데이터베이스 미러링 엔드포인트에서 연결 인증을 거부했음을 보고합니다. Windows 인증일 경우 이 이벤트는 연결의 보안 식별자가 데이터베이스 사용자와 일치하지 않음을 보고합니다. 인증서 기반 인증일 경우 이 이벤트는 메시지에 전달된 공개 키가 **master** 데이터베이스의 인증서와 맞지 않음을 보고합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [CREATE ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [ALTER ENDPOINT&#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
