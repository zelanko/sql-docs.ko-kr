---
title: CONNECTIONPROPERTY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CONNECTIONPROPERTY_TSQL
- CONNECTIONPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- CONNECTIONPROPERTY statement
ms.assetid: 6bd9ccae-af77-4a05-b97f-f8ab41cfde42
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 53b447b2a13c68c2c87536bc3c1f14f9efd74cfd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132094"
---
# <a name="connectionproperty-transact-sql"></a>CONNECTIONPROPERTY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

서버에 들어오는 요청의 경우 이 함수는 해당 요청을 지원하는 고유한 연결의 연결 속성에 대한 정보를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
CONNECTIONPROPERTY ( property )  
```  
  
## <a name="arguments"></a>인수  
*property*  
연결의 속성입니다. *property*에는 다음 값 중 하나가 있을 수 있습니다.
  
|값|데이터 형식|설명|  
|---|---|---|
|net_transport|**nvarchar(40)**|이 연결에서 사용하는 물리적 전송 프로토콜을 반환합니다. 이 값은 null을 허용하지 않습니다. 가능한 반환 값:<br /><br /> **HTTP**<br /> **명명된 파이프**<br /> **세션**<br /> **공유 메모리**<br /> **SSL**<br /> **TCP**<br /><br /> 및<br /><br /> **VIA**<br /><br /> 참고: 연결에 MARS(Multiple Active Result Sets)가 모두 설정되고 연결 풀링이 사용되는 경우 항상 **세션**을 반환합니다.|  
|protocol_type|**nvarchar(40)**|페이로드 프로토콜 형식을 반환합니다. 현재 TDS(TSQL)와 SOAP을 구분합니다. Null을 허용합니다.|  
|auth_scheme|**nvarchar(40)**|연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 체계를 반환합니다. 인증 체계는 Windows 인증(NTLM, KERBEROS, DIGEST, BASIC, NEGOTIATE) 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증입니다. Null을 허용하지 않습니다.|  
|local_net_address|**varchar(48)**|이 특정 연결이 대상으로 하는 서버의 IP 주소를 반환합니다. TCP 전송 공급자를 사용하는 연결의 경우에만 지원됩니다. Null을 허용합니다.|  
|local_tcp_port|**int**|TCP 전송을 사용하는 연결인 경우 이 연결이 대상으로 하는 서버 TCP 포트를 반환합니다. Null을 허용합니다.|  
|client_net_address|**varchar(48)**|이 서버에 연결하려는 클라이언트의 주소를 요청합니다. Null을 허용합니다.|  
|physical_net_transport|**nvarchar(40)**|이 연결에서 사용하는 물리적 전송 프로토콜을 반환합니다. 연결에 MARS(Multiple Active Result Sets)가 설정된 경우 정확합니다.|  
|\<다른 문자열>||잘못된 입력에 NULL을 반환합니다.|  
  
## <a name="remarks"></a>Remarks  
**local_net_address** 및 **local_tcp_port**는 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]에서 NULL을 반환합니다.
  
반환된 값은 [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md) 동적 관리 뷰에서 해당 열에 대해 표시되는 옵션과 일치합니다. 예를 들어
  
```sql
SELECT   
ConnectionProperty('net_transport') AS 'Net transport',   
ConnectionProperty('protocol_type') AS 'Protocol type';  
```  
  
## <a name="see-also"></a>관련 항목:
[sys.dm_exec_sessions&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
[sys.dm_exec_requests&#40;Transact-SQL&#41](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)
  
  
