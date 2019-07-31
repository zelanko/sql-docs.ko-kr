---
title: '진행률 보고서: Online Index Operation 이벤트 클래스 | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 'Progress Report: Online Index Operation event class [SQL Server]'
ms.assetid: 491616c1-f666-4b16-a5ea-1192bf156692
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a9388483151326222dd8fa5e085467b15600eca9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67940648"
---
# <a name="progress-report-online-index-operation-event-class"></a>진행률 보고서: Online Index Operation 이벤트 클래스
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Progress Report: Online Index Operation 이벤트 클래스는 온라인 인덱스 작성 작업을 진행하는 동안 온라인 인덱스 작성 진행률을 나타냅니다.  
  
## <a name="progress-report-online-index-operation-event-class-data-columns"></a>진행률 보고서: Online Index Operation 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|설명|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|예|  
|BigintData1|**bigint**|삽입된 행 수|52|예|  
|BigintData2|**bigint**|0 = 직렬 계획, 그렇지 않은 경우 - 병렬 실행 중의 스레드 ID|53|예|  
|ClientProcessID|**int**|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|DatabaseID|**int**|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에 ServerName 데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|DatabaseName|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|예|  
|Duration|**bigint**|이벤트에 의해 사용된 시간(마이크로초)입니다.|13|예|  
|EndTime|**datetime**|온라인 인덱스 작업이 완료된 시간입니다.|15|예|  
|EventClass|**int**|이벤트 유형 = 190|27|아니오|  
|EventSequence|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|아니오|  
|EventSubClass|**int**|이벤트 하위 클래스의 유형입니다.<br /><br /> 1=시작<br /><br /> 2=단계 1 실행 시작<br /><br /> 3=단계 1 실행 종료<br /><br /> 4=2단계 실행 시작<br /><br /> 5=2단계 실행 종료<br /><br /> 6=삽입된 행 수<br /><br /> 7=완료<br /><br /> 1단계는 기준 개체(클러스터형 인덱스 또는 힙)를 참조하거나 인덱스 작업에 하나의 비클러스터형 인덱스만 포함될 경우 수행됩니다. 2단계는 인덱스 작성 작업에 원래의 다시 작성과 추가 비클러스터형 인덱스가 모두 포함될 경우에 사용됩니다.  예를 들어 개체에 하나의 클러스터형 인덱스와 7개의 비클러스터형 인덱스가 있을 경우 'rebuild all' 명령은 모든 인덱스를 다시 작성합니다. 기준 개체(클러스터형 인덱스)는 1단계에서 다시 작성되며 그런 다음 2단계에서 모든 비클러스터형 인덱스가 다시 작성됩니다.|21|예|  
|GroupID|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|예|  
|HostName|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|IndexID|**int**|이벤트에 의해 영향 받는 개체의 인덱스 ID입니다.|24|예|  
|IsSystem|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|LoginName|**nvarchar**|사용자 로그인 이름이며 DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인입니다.|11|예|  
|LoginSid|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|NTDomainName|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|NTUserName|**nvarchar**|Windows 사용자 이름입니다.|6|예|  
|ObjectID|**int**|시스템이 할당한 개체의 ID입니다.|22|예|  
|ObjectName|**nvarchar**|참조되는 개체의 이름입니다.|34|예|  
|PartitionId|**bigint**|작성 중인 파티션의 ID입니다.|65|예|  
|PartitionNumber|**int**|작성 중인 파티션의 일반 번호입니다.|25|예|  
|데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|아니오|  
|SessionLoginName|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|SPID|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다.|14|예|  
|TransactionID|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|예|  
  
## <a name="see-also"></a>참고 항목  
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
