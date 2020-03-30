---
title: SP:CacheInsert 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- SP:CacheInsert event class
ms.assetid: 37fb9bec-b462-4563-8e50-ec84d5407e20
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 35af49d1c01908dbbea2778125636c1424819ebf
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67910949"
---
# <a name="spcacheinsert-event-class"></a>SP:CacheInsert 이벤트 클래스
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  SP:CacheInsert 이벤트 클래스는 저장 프로시저가 프로시저 캐시에 삽입되었음을 나타냅니다.  
  
## <a name="spcacheinsert-event-class-data-columns"></a>SP:CacheInsert 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|yes|  
|ClientProcessID|**int**|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|yes|  
|DatabaseID|**int**|저장 프로시저가 실행되는 데이터베이스의 ID입니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|yes|  
|DatabaseName|**nvarchar**|저장 프로시저가 실행되는 데이터베이스의 이름입니다.|35|yes|  
|EventClass|**int**|이벤트 유형 = 35|27|예|  
|EventSequence|**int**|요청 내의 지정된 이벤트 시퀀스입니다.|51|예|  
|GroupID|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|yes|  
|HostName|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|yes|  
|IsSystem|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|yes|  
|LoginName|**nvarchar**|사용자 로그인 이름이며 DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인입니다.|11|yes|  
|LoginSid|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|yes|  
|NTDomainName|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|yes|  
|NTUserName|**nvarchar**|Windows 사용자 이름입니다.|6|yes|  
|ObjectID|**int**|시스템이 할당한 저장 프로시저의 ID입니다.|22|yes|  
|ObjectType|**int**|이벤트와 관련된 개체 유형을 나타내는 값입니다. 이 값은 sys.objects 카탈로그 뷰의 유형 열과 일치합니다. 값은 [ObjectType 추적 이벤트 열](../../relational-databases/event-classes/objecttype-trace-event-column.md)을 참조하세요.|28|yes|  
|RequestID|**int**|문을 포함하는 요청의 ID입니다.|49|yes|  
|ServerName|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|예|  
|SessionLoginName|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 Windows 로그인이 모두 표시됩니다.|64|yes|  
|SPID|**int**|이벤트가 발생한 세션의 ID입니다.|12|yes|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|yes|  
|TextData|**ntext**|캐시된 SQL 코드 텍스트입니다.|1|yes|  
|TransactionID|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|yes|  
|XactSequence|**bigint**|현재 트랜잭션을 설명하는 토큰입니다.|50|yes|  
  
## <a name="see-also"></a>참고 항목  
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [SP:CacheMiss 이벤트 클래스](../../relational-databases/event-classes/sp-cachemiss-event-class.md)  
  
  
