---
title: CONNECTIONPROPERTY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CONNECTIONPROPERTY_TSQL
- CONNECTIONPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- CONNECTIONPROPERTY statement
ms.assetid: 6bd9ccae-af77-4a05-b97f-f8ab41cfde42
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2a5b023530bce0269af96918b0d578c6ca54293d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="connectionproperty-transact-sql"></a>CONNECTIONPROPERTY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

요청이 들어 오는 고유한 연결의 연결 속성에 대한 정보를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
CONNECTIONPROPERTY ( property )  
```  
  
## <a name="arguments"></a>인수  
*속성*  
연결의 속성입니다. *속성* 다음 값 중 하나일 수 있습니다.
  
|값|데이터 형식|Description|  
|---|---|---|
|net_transport|**nvarchar (40)**|이 연결에서 사용하는 물리적 전송 프로토콜을 반환합니다. Null을 허용하지 않습니다.<br /><br /> 반환 값은: **HTTP**, **명명 된 파이프**, **세션**, **공유 메모리**, **SSL**, **TCP**, 및 **VIA**합니다.<br /><br /> 참고: 항상 반환 **세션** 연결 multiple active result sets (MARS) 설정,이 고 연결 풀링이 사용 하도록 설정 된 경우.|  
|protocol_type|**nvarchar (40)**|페이로드의 프로토콜 유형을 반환합니다. 현재 TDS(TSQL)와 SOAP을 구분합니다. Null을 허용합니다.|  
|auth_scheme|**nvarchar (40)**|반환 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결에 대 한 인증 체계입니다. 인증 체계는 Windows 인증(NTLM, KERBEROS, DIGEST, BASIC, NEGOTIATE) 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증입니다. Null을 허용하지 않습니다.|  
|local_net_address|**varchar(48)**|이 연결이 대상으로 하는 서버의 IP 주소를 반환합니다. TCP 전송 공급자를 사용하여 연결한 경우에만 사용할 수 있습니다. Null을 허용합니다.|  
|local_tcp_port|**int**|TCP 전송을 사용하는 연결인 경우 이 연결이 대상으로 하는 서버 TCP 포트를 반환합니다. Null을 허용합니다.|  
|client_net_address|**varchar(48)**|이 서버에 연결되는 클라이언트의 주소를 요청합니다. Null을 허용합니다.|  
|physical_net_transport|**nvarchar (40)**|이 연결에서 사용하는 물리적 전송 프로토콜을 반환합니다. 연결에 MARS(Multiple Active Result Sets)가 설정된 경우 정확합니다.|  
|\<다른 문자열 >||입력이 유효하지 않으면 NULL을 반환합니다.|  
  
## <a name="remarks"></a>주의  
**local_net_address** 및 **local_tcp_port** 에서 NULL을 반환 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]합니다.
  
반환 되는 값의 해당 열에 대 한 표시 옵션으로 같습니다는 [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md) 동적 관리 뷰. 예를 들어
  
```sql
SELECT   
ConnectionProperty('net_transport') AS 'Net transport',   
ConnectionProperty('protocol_type') AS 'Protocol type';  
```  
  
## <a name="see-also"></a>참고 항목
[sys.dm_exec_sessions&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
[sys.dm_exec_requests &#40; Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)
  
  

