---
description: Lock:Cancel 이벤트 클래스
title: Lock:Cancel 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Cancel event class
ms.assetid: d9203e58-40ba-4712-a918-2c34a5d396d7
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7ac6f7773736f09368825e89a5b0b6707ad0d176
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97485415"
---
# <a name="lockcancel-event-class"></a>Lock:Cancel 이벤트 클래스
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **Lock:Cancel** 이벤트 클래스는 쿼리 취소 등의 원인으로 리소스에 대한 잠금 획득이 취소되었음을 나타냅니다.  
  
## <a name="lockcancel-event-class-data-columns"></a>Lock:Cancel 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|예|  
|**BinaryData**|**image**|잠금 리소스 식별자입니다.|2|예|  
|**ClientProcessID**|**int**|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|**DatabaseID**|**int**|잠금을 획득한 데이터베이스의 ID입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|**DatabaseName**|**nvarchar**|잠금 획득이 시도된 데이터베이스의 이름입니다.|35|예|  
|**Duration**|**bigint**|잠금 요청 실행과 잠금 취소 사이의 시간(마이크로초)입니다.|13|예|  
|**EndTime**|**datetime**|이벤트가 종료된 시간입니다.|15|예|  
|**EventClass**|**int**|이벤트 유형 = 26|27|예|  
|**EventSequence**|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|예|  
|**GroupID**|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|예|  
|**HostName**|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|**IntegerData2**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|55|예|  
|**IsSystem**|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|**LoginName**|**nvarchar**|사용자 로그인 이름이며 DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인입니다.|11|예|  
|**LoginSid**|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 **sys.server_principals** 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|**모드**|**int**|잠금이 취소된 다음의 결과 모드입니다.<br /><br /> 0=NULL - 모든 잠금 모드와 호환(LCK_M_NL)<br /><br /> 1=스키마 안정성 잠금(LCK_M_SCH_S)<br /><br /> 2=스키마 수정 잠금(LCK_M_SCH_M)<br /><br /> 3=공유 잠금(LCK_M_S)<br /><br /> 4=업데이트 잠금(LCK_M_U)<br /><br /> 5=배타 잠금(LCK_M_X)<br /><br /> 6=내재된 공유 잠금(LCK_M_IS)<br /><br /> 7=의도 업데이트 잠금(LCK_M_IU)<br /><br /> 8=의도 배타 잠금(LCK_M_IX)<br /><br /> 9=의도 업데이트 공유(LCK_M_SIU)<br /><br /> 10=의도 배타 공유(LCK_M_SIX)<br /><br /> 11=의도 배타 업데이트(LCK_M_UIX)<br /><br /> 12=대량 업데이트 잠금(LCK_M_BU)<br /><br /> 13=키 범위 공유/공유(LCK_M_RS_S)<br /><br /> 14=키 범위 공유/업데이트(LCK_M_RS_U)<br /><br /> 15=키 범위 삽입 NULL(LCK_M_RI_NL)<br /><br /> 16=키 범위 삽입 공유(LCK_M_RI_S)<br /><br /> 17=키 범위 삽입 업데이트(LCK_M_RI_U)<br /><br /> 18=키 범위 삽입 배타(LCK_M_RI_X)<br /><br /> 19=키 범위 배타 공유(LCK_M_RX_S)<br /><br /> 20=키 범위 배타 업데이트(LCK_M_RX_U)<br /><br /> 21=키 범위 배타 배타(LCK_M_RX_X)|32|예|  
|**NTDomainName**|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|**NTUserName**|**nvarchar**|Windows 사용자 이름입니다.|6|예|  
|**Exchange Spill**|**int**|잠금이 취소된 개체의 ID입니다(사용 및 적용 가능한 경우).|22|예|  
|**ObjectID2**|**bigint**|관련 개체 또는 엔터티의 ID입니다(사용 및 적용 가능한 경우).|56|예|  
|**OwnerID**|**int**|1=TRANSACTION<br /><br /> 2=CURSOR<br /><br /> 3=SESSION<br /><br /> 4=SHARED_TRANSACTION_WORKSPACE<br /><br /> 5=EXCLUSIVE_TRANSACTION_WORKSPACE|58|예|  
|**RequestID**|**int**|문을 포함하는 요청의 ID입니다.|49|예|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|예|  
|**SessionLoginName**|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 **SessionLoginName** 은 Login1을 표시하고 **LoginName** 은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|**SPID**|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|**StartTime**|**datetime**|사용 가능한 경우 이벤트가 시작된 시간입니다.|14|예|  
|**TextData**|**ntext**|획득한 잠금 유형에 따라 달라지는 텍스트 값입니다. 이 값은 **sys.dm_tran_locks** 의 **resource_description** 열과 같습니다.|1|예|  
|**TransactionID**|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|예|  
|**형식**|**int**|1=NULL_RESOURCE<br /><br /> 2=DATABASE<br /><br /> 3=FILE<br /><br /> 5=OBJECT<br /><br /> 6=PAGE<br /><br /> 7=KEY<br /><br /> 8=EXTENT<br /><br /> 9=RID<br /><br /> 10=APPLICATION<br /><br /> 11=METADATA<br /><br /> 12=AUTONAMEDB<br /><br /> 13=HOBT<br /><br /> 14=ALLOCATION_UNIT|57|예|  
  
## <a name="see-also"></a>참고 항목  
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sys.dm_tran_locks&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)  
  
  
