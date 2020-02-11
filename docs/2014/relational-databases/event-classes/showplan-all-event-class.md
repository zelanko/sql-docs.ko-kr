---
title: Showplan All 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Showplan All event class
ms.assetid: ee341319-c34a-43e3-ad33-6bfb1f85e314
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 487aaee17be13727f2c23de42b95afcc27b0b939
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62662197"
---
# <a name="showplan-all-event-class"></a>Showplan All 이벤트 클래스
  실행 계획 All 이벤트 클래스는가 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL 문을 실행할 때 발생 합니다. 여기서 설명하는 내용은 Showplan XML Statistics Profile 또는 Showplan XML 이벤트 클래스에서 사용할 수 있는 정보의 일부입니다.  
  
 Showplan All 이벤트 클래스는 완전한 컴파일 시간 데이터를 표시하므로 Showplan All을 포함하는 추적은 상당한 성능 오버헤드를 발생시킬 수 있습니다. 이 문제를 최소화하려면 단기간 동안 특정 문제를 모니터링하는 추적에서만 이 이벤트 클래스를 사용하십시오.  
  
 추적에 Showplan All 이벤트 클래스가 포함되면 BinaryData 데이터 열을 선택해야 합니다. 그렇지 않을 경우 이 이벤트 클래스에 대한 정보가 추적에 표시되지 않습니다.  
  
## <a name="showplan-all-event-class-data-columns"></a>Showplan All 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|yes|  
|BinaryData|`image`|Showplan 텍스트의 예상 비용입니다.|2|예|  
|ClientProcessID|`int`|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|yes|  
|DatabaseID|`Int`|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]ServerName 데이터 열이 추적에서 캡처되고 서버를 사용할 수 있는 경우 데이터베이스의 이름을 표시 합니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|yes|  
|DatabaseName|`nvarchar`|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|yes|  
|Event Class|`Int`|이벤트 유형 = 97|27|예|  
|EventSequence|`int`|요청 내에 지정된 이벤트 시퀀스입니다.|51|예|  
|GroupID|`int`|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|yes|  
|HostName|`nvarchar`|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|yes|  
|Integer Data|`Integer`|반환한 행의 예상 개수입니다.|25|yes|  
|IsSystem|`int`|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|yes|  
|LineNumber|`int`|오류를 포함하는 줄 번호를 표시합니다.|5|yes|  
|LoginName|`nvarchar`|사용자 로그인 이름(DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인)입니다.|11|yes|  
|LoginSID|`image`|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|NestLevel|`int`|@@NESTLEVEL에서 반환한 데이터를 나타내는 정수입니다.|29|yes|  
|NTDomainName|`nvarchar`|사용자가 속한 Windows 도메인입니다.|7|yes|  
|ObjectID|`int`|시스템이 할당한 개체의 ID입니다.|22|yes|  
|ObjectName|`nvarchar`|참조되는 개체의 이름입니다.|34|yes|  
|ObjectType|`int`|이벤트와 관련된 개체 유형을 나타내는 값입니다. 이 값은 sys.objects의 유형 열과 일치합니다. 값은 [ObjectType 추적 이벤트 열](objecttype-trace-event-column.md)을 참조하세요.|28|yes|  
|RequestID|`int`|문을 포함하는 요청의 ID입니다.|49|yes|  
|ServerName|`nvarchar`|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|예|  
|SessionLoginName|`nvarchar`|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|yes|  
|SPID|`int`|이벤트가 발생한 세션의 ID입니다.|12|yes|  
|StartTime|`datetime`|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|yes|  
|TransactionID|`bigint`|시스템이 할당한 트랜잭션의 ID입니다.|4|yes|  
|XactSequence|`bigint`|현재 트랜잭션을 설명하는 토큰입니다.|50|yes|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 프로파일러](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [실행 계획 논리 및 물리 연산자 참조](../showplan-logical-and-physical-operators-reference.md)   
 [실행 계획 XML Statistics Profile 이벤트 클래스](showplan-xml-statistics-profile-event-class.md)   
 [Showplan XML 이벤트 클래스](showplan-xml-event-class.md)  
  
  
