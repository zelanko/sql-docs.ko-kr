---
title: 복제 에이전트 이벤트에 대한 경고 사용 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- viewing alerts
- Queue Reader Agent, alerts
- alerts [SQL Server replication]
- predefined replication alerts [SQL Server replication]
- Log Reader Agent, alerts
- Distribution Agent, alerts
- Merge Agent, alerts
- agents [SQL Server replication], alerts
- displaying alerts
- Snapshot Agent, alerts
ms.assetid: 8c42e523-7020-471d-8977-a0bd044b9471
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3a670a78f6e906221638fb67c1cf5be8398b415b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52762585"
---
# <a name="use-alerts-for-replication-agent-events"></a>복제 에이전트 이벤트에 대한 경고 사용
  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 및 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트에서는 경고를 사용하여 복제 에이전트 이벤트 등의 이벤트를 모니터링하는 방법을 제공합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트는 경고와 관련된 이벤트에 대한 Windows 응용 프로그램 로그를 모니터링합니다. 이런 이벤트가 발생하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트는 사용자가 정의한 태스크를 실행하거나 지정된 운영자에게 전자 메일 또는 호출기 메시지를 보내어 자동으로 응답합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에는 태스크를 실행하거나 운영자에게 알리도록 구성할 수 있는 복제 에이전트에 대한 미리 정의된 경고 집합이 포함되어 있습니다. 실행할 태스크를 정의하는 방법은 이 항목의 "경고에 대한 응답 자동화" 섹션을 참조하십시오.  
  
 컴퓨터가 배포자로 구성될 때는 다음과 같은 경고가 설치됩니다.  
  
|메시지 ID|미리 정의된 경고|경고가 발생되는 조건|msdb..sysreplicationalerts에 추가 정보 입력|  
|----------------|----------------------|-----------------------------------------|-----------------------------------------------------------------|  
|14150|**복제: 에이전트 성공**|에이전트가 성공적으로 종료됩니다.|사용자 계정 컨트롤|  
|14151|**복제: 에이전트 실패**|오류로 인해 에이전트가 종료됩니다.|사용자 계정 컨트롤|  
|14152|**복제: 에이전트 다시 시도**|불필요한 작업을 다시 시도한 후 에이전트가 종료합니다. 에이전트에는 사용할 수 없는 서버, 교착 상태, 연결 실패, 제한 시간 실패 등이 발생합니다.|사용자 계정 컨트롤|  
|14157|**복제: 만료된 구독 삭제**|만료된 구독이 삭제되었습니다.|아니요|  
|20572|**복제: 구독 유효성 검사 실패 후 다시 초기화**|'데이터 유효성 검사 실패 시 구독 다시 초기화' 응답 작업이 구독을 성공적으로 다시 초기화합니다.|아니요|  
|20574|**복제: 구독자가 데이터 유효성 검사에 실패 했습니다.**|배포 또는 병합 에이전트가 데이터 유효성 검사에 실패합니다.|사용자 계정 컨트롤|  
|20575|**복제: 구독자에서 데이터 유효성 검사를 통과 했습니다.**|배포 또는 병합 에이전트가 데이터 유효성 검사를 통과합니다.|사용자 계정 컨트롤|  
|20578|**복제: 에이전트 사용자 지정 종료**|||  
|22815|**피어 투 피어 충돌 감지 경고**|피어 투 피어 노드에서 변경 내용을 적용하려고 할 때 배포 에이전트에서 충돌이 감지되었습니다.|사용자 계정 컨트롤|  
  
 복제 모니터는 이러한 경고 외에도 상태 및 성능과 관련된 일련의 경고를 제공합니다. 자세한 내용은 [임계값 설정 및 복제 모니터에서 경고](../monitor/set-thresholds-and-warnings-in-replication-monitor.md) 경고 인프라입니다. 자세한 내용은 [사용자 정의 이벤트 만들기](../../../ssms/agent/create-a-user-defined-event.md)를 참조하세요.  
  
 **미리 정의된 복제 경고를 구성하려면**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [미리 정의 된 복제 경고 구성 &#40;SQL Server Management Studio&#41;](../administration/configure-predefined-replication-alerts-sql-server-management-studio.md)  
  
## <a name="viewing-the-application-log-directly"></a>애플리케이션 로그 직접 보기  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 이벤트 뷰어를 사용하여 Windows 응용 프로그램 로그를 볼 수 있습니다. 애플리케이션 로그에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 오류 메시지는 물론, 해당 컴퓨터에서 이루어지는 다른 여러 동작에 대한 메시지도 포함됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 오류 로그와 달리 새 응용 프로그램 로그는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 시작할 때마다 생성되지 않고 각 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 세션이 새 이벤트를 기존 응용 프로그램 로그에 기록하지만 로그된 이벤트를 유지할 기간을 지정할 수 있습니다. Windows 애플리케이션 로그를 보고 특정 이벤트에 대한 로그를 필터링할 수 있습니다. 자세한 내용은 Windows 설명서를 참조하십시오.  
  
## <a name="automating-a-response-to-an-alert"></a>경고에 대한 응답 자동화  
 복제 시 데이터 유효성 검사에 실패한 구독에 대한 응답 작업을 제공하며 경고에 대한 자동 응답을 추가로 만드는 프레임워크 또한 제공합니다. 응답 작업은 **데이터 유효성 검사 실패 시 구독 다시 초기화** 로 제목이 지정되고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 **에이전트** 작업 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]폴더에 저장됩니다. 이 응답 작업을 사용하도록 설정하는 방법은 [미리 정의된 복제 경고 구성&#40;SQL Server Management Studio&#41;](../administration/configure-predefined-replication-alerts-sql-server-management-studio.md)을 참조하세요. 트랜잭션 게시의 아티클이 유효성 검사에 실패하면 응답 작업은 실패한 아티클만 다시 초기화합니다. 병합 게시의 아티클이 유효성 검사에 실패하면 응답 작업은 게시의 모든 아티클을 다시 초기화합니다.  
  
### <a name="framework-for-automating-responses"></a>응답 자동화를 위한 프레임워크  
 일반적으로 경고가 발생하면 경고가 발생한 원인과 적절한 조치를 이해하는 데 도움이 되는 유일한 정보는 경고 메시지에 포함되어 있습니다. 이 정보를 구문 분석하면 오류가 발생하고 시간이 많이 걸릴 수 있습니다. 복제는 **sysreplicationalerts** 시스템 테이블의 경고에 대한 추가 정보를 제공하여 응답을 쉽게 자동화할 수 있게 해줍니다. 제공된 정보는 사용자 지정된 프로그램에서 쉽게 사용할 수 있도록 정보를 이미 구문 분석된 형태로 제공합니다.  
  
 예를 들어 A 구독자의 **Sales.SalesOrderHeader** 테이블에 있는 데이터가 유효성 검사에 실패하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 사용자에게 해당 오류를 알리는 메시지 20574를 발생시킬 수 있습니다. 나타날 수 있는 메시지는 다음과 같습니다. "게시 'MyPublication'의 아티클 'SalesOrderHeader'에 대한 구독자 'A'의 구독이 데이터 유효성 검사에 실패했습니다."  
  
 메시지를 기반으로 응답을 만들 때는 메시지에서 구독자 이름, 아티클 이름, 게시 이름 및 오류 등을 수동으로 구문 분석해야 합니다. 그러나 배포 에이전트와 병합 에이전트가 동일한 정보를 에이전트 유형, 경고 시간, 게시 데이터베이스, 구독자 데이터베이스, 게시 유형과 같은 자세한 정보와 함께 **sysreplicationalerts** 에 기록하므로, 응답 작업은 관련 정보를 테이블에서 직접 쿼리할 수 있습니다. 경고의 특정 인스턴스에 정확한 행이 관련될 수는 없더라도 테이블에는 서비스된 항목을 추적할 때 사용할 수 있는 **status** 열이 있습니다. 이 테이블의 항목들은 기록 보존 기간 동안 유지 관리됩니다.  
  
 예를 들어 경고 메시지 20574를 서비스하는 응답 작업을 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 로 작성하려는 경우에는 다음과 같은 논리를 사용할 수 있습니다.  
  
```  
declare @publisher sysname, @publisher_db sysname, @publication sysname, @publication_type int, @article sysname, @subscriber sysname, @subscriber_db sysname, @alert_id int  
declare hc cursor local for select publisher, publisher_db, publication, publication_type, article, subscriber,   
  subscriber_db, alert_id from   
  msdb..sysreplicationalerts where  
  alert_error_code = 20574 and status = 0  
  for read only  
open hc  
fetch hc into  @publisher, @publisher_db, @publication, @publication_type, @article, @subscriber, @subscriber_db, @alert_id  
while (@@fetch_status <> -1)  
begin  
/* Do custom work  */  
/* Update status to 1, which means the alert has been serviced. This prevents subsequent runs of this job from doing this again */  
update msdb..sysreplicationalerts set status = 1 where alert_id = @alert_id  
 fetch hc into  @publisher, @publisher_db, @publication, @publication_type, @article, @subscriber, @subscriber_db, @alert_id  
end  
close hc  
deallocate hc  
```  
  
## <a name="see-also"></a>관련 항목  
 [복제 에이전트 관리](replication-agent-administration.md)   
 [Best Practices for Replication Administration](../administration/best-practices-for-replication-administration.md)   
 [모니터링&#40;복제&#41;](../monitoring-replication.md)  
  
  
