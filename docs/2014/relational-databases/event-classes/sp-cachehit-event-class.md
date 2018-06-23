---
title: SP:CacheHit 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
topic_type:
- apiref
helpviewer_keywords:
- SP:CacheHit event class
ms.assetid: 396aa22a-4723-47f5-ae72-7de99d92dd6f
caps.latest.revision: 41
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 34a0a8beba7b9d8f0ac667777ce0d7c0b8587294
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36185189"
---
# <a name="spcachehit-event-class"></a>SP:CacheHit 이벤트 클래스
  SP:CacheHit 이벤트 클래스는 저장 프로시저가 계획 캐시에 있음을 나타냅니다.  
  
## <a name="spcachehit-event-class-data-columns"></a>SP:CacheHit 이벤트 클래스 데이터 열  
  
|데이터 열 이름|`Data type`|Description|열 ID|필터 가능|  
|----------------------|-------------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|10|예|  
|ClientProcessID|`int`|클라이언트 응용 프로그램이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|DatabaseID|`int`|저장 프로시저가 실행되는 데이터베이스의 ID입니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|DatabaseName|`nvarchar`|저장 프로시저가 실행되는 데이터베이스의 이름입니다.|35|예|  
|EventClass|`int`|이벤트 유형 = 38|27|아니요|  
|EventSequence|`int`|요청 내의 지정된 이벤트 시퀀스입니다.|51|아니요|  
|EventSubClass|`int`|이벤트 하위 클래스의 형식입니다.<br /><br /> 1=Execution Context Hit: 계획 캐시에 사용 가능한 실행 계획이 있습니다.<br /><br /> 2=Compplan Hit: 계획 캐시에 컴파일된 계획이 있습니다.|21|예|  
|GroupID|`int`|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|예|  
|HostName|`nvarchar`|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|IsSystem|`int`|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|LoginName|`nvarchar`|사용자 로그인 이름이며 DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인입니다.|11|예|  
|LoginSid|`image`|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|NTDomainName|`nvarchar`|사용자가 속한 Windows 도메인입니다.|7|예|  
|NTUserName|`nvarchar`|Windows 사용자 이름입니다.|6|예|  
|ObjectID|`int`|캐시에서 발견된 시스템이 할당한 저장 프로시저의 ID입니다.|22|예|  
|ObjectName|`nvarchar`|캐시에서 발견된 개체의 이름입니다. ObjectName이 채워지면 TextData는 채워지지 않습니다.|34|예|  
|ObjectType|`int`|이벤트와 관련된 개체 유형을 나타내는 값입니다. 이 값은 sys.objects 카탈로그 뷰의 유형 열과 일치합니다. 값은 [ObjectType 추적 이벤트 열](objecttype-trace-event-column.md)을 참조하세요.|28|예|  
|RequestID|`int`|문을 포함하는 요청의 ID입니다.|49|예|  
|데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면|`nvarchar`|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|아니요|  
|SessionLoginName|`nvarchar`|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|SPID|`int`|이벤트가 발생한 세션의 ID입니다.|12|예|  
|StartTime|`datetime`|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|TextData|`ntext`|캐시에서 발견된 SQL 코드의 텍스트입니다. TextData가 채워지면 ObjectName은 채워지지 않습니다.|1|예|  
|TransactionID|`bigint`|시스템이 할당한 트랜잭션의 ID입니다.|4|예|  
|XactSequence|`bigint`|현재 트랜잭션을 설명하는 토큰입니다.|50|예|  
  
## <a name="see-also"></a>관련 항목  
 [sp_trace_setevent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
