---
title: SQL Server Service Broker | Microsoft Docs
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.SWB.SSBMSGTYPEPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBCONTRACTPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBQUEUEPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBREMSVCBINDPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBROUTEPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBPRIORITYPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBSERVICEPROPERTIES.GENERAL.F1
helpviewer_keywords:
- Broker See Service Broker
- SQL Server Service Broker
- Service Broker
ms.assetid: 8b8b3b57-fd46-44de-9a4e-e3a8e3999c1e
caps.latest.revision: "22"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: 20407c3b614ed6e977e2ba69ba687b75f7d18fdf
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-service-broker"></a>SQL Server Service Broker
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 메시징 및 큐 응용 프로그램에 대한 기본 지원을 제공합니다. 이러한 지원을 통해 개발자는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 구성 요소를 사용하여 서로 다른 데이터베이스 간에 통신하는 복잡한 응용 프로그램을 쉽게 만들 수 있습니다. 개발자는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 를 사용하여 신뢰할 수 있는 분산 응용 프로그램을 간단하게 작성할 수 있습니다.  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 를 사용하는 응용 프로그램 개발자는 복잡한 통신 및 메시징 내부 사항을 프로그래밍하지 않고도 데이터 작업을 여러 데이터베이스에 분산시킬 수 있습니다. 이렇게 하면 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 가 대화 컨텍스트에서 통신 경로를 처리하므로 개발 및 테스트 작업이 줄어들 뿐만 아니라 성능이 향상됩니다. 예를 들어, 웹 사이트를 지원하는 프런트 엔드 데이터베이스는 정보를 기록하고 프로세스를 많이 사용하는 태스크를 백 엔드 데이터베이스의 큐로 보낼 수 있습니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)] 는 모든 태스크가 트랜잭션 컨텍스트에서 관리되도록 하여 안정성과 기술 일관성을 유지합니다.  
  
## <a name="where-is-the-documentation-for-service-broker"></a>Service Broker 설명서의 위치  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 에 대한 참조 설명서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설명서에 포함되어 있습니다. 이 참조 설명서는 다음과 같은 섹션으로 구성됩니다.  
  
-   CREATE, ALTER 및 DROP 문에 대한 [DDL&#40;데이터 정의 언어&#41; 문&#40;Transact-SQL&#41;](~/mdx/mdx-data-definition-statements-mdx.md)  
  
-   [Service Broker 문](../../t-sql/statements/service-broker-statements.md)  
  
-   [Service Broker 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/service-broker-catalog-views-transact-sql.md)  
  
-   [Service Broker 관련 동적 관리 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
-   [ssbdiagnose 유틸리티&#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
 [개념과 개발 및 관리 태스크에 대한 자세한 내용은](http://go.microsoft.com/fwlink/?LinkId=231312) 이전에 게시된 설명서 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 를 참조하십시오. 이 설명서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 의 변경 사항이 적기 때문에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]설명서에서 다시 작성되지 않았습니다.  
  
## <a name="whats-new-in-service-broker"></a>Service Broker의 새로운 기능  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에 도입된 큰 변경 내용은 없습니다.  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서의 변경 내용은 다음과 같습니다.  
  
### <a name="messages-can-be-sent-to-multiple-target-services-multicast"></a>메시지를 여러 대상 서비스에 보낼 수 있음(멀티캐스트)  
 [SEND&#40;Transact-SQL&#41;](../../t-sql/statements/send-transact-sql.md) 문의 구문은 여러 대화 핸들을 지원하여 멀티캐스트를 설정하기 위해 확장되었습니다.  
  
### <a name="queues-expose-the-message-enqueued-time"></a>메시지가 큐에 유지된 시간이 큐에서 노출됨  
 메시지가 큐에 유지된 시간을 보여 주는 **message_enqueue_time**이라는 새 열이 큐에 있습니다.  
  
### <a name="poison-message-handling-can-be-disabled"></a>포이즌 메시지 처리를 해제할 수 있음  
 [CREATE QUEUE&#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md) 및 [ALTER QUEUE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-queue-transact-sql.md) 문은 이제 `POISON_MESSAGE_HANDLING (STATUS = ON | OFF)` 절을 추가하여 포이즌 메시지 처리를 설정하거나 해제할 수 있습니다. 카탈로그 뷰 **sys.service_queues** 에는 이제 포이즌 메시지가 설정되었는지, 아니면 해제되었는지를 나타내는 **is_poison_message_handling_enabled** 열이 있습니다.  
  
### <a name="always-on-support-in-service-broker"></a>Service Broker의 Always On 지원  
 자세한 내용은 [Always On 가용성 그룹이 포함된 Service Broker(SQL Server)](../../database-engine/availability-groups/windows/service-broker-with-always-on-availability-groups-sql-server.md)를 참조하세요.  
  
  

