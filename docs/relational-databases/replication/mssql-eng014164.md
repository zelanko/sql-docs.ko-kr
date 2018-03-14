---
title: "MSSQL_ENG014164 | Microsoft 문서"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG014164 error
ms.assetid: cd81b601-2ec3-4358-ad58-c2655496e6a1
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f21a00a649bab08678f063a6aeb11804d454731c
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="mssqleng014164"></a>MSSQL_ENG014164
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|14164|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|게시 [%s]에 대한 임계값 [%s:%s]이(가) 설정되어 있습니다. 병합 에이전트가 실행 중이고 필요한 요구 사항에 맞는지 확인하십시오. 병합 에이전트가 실행 중이고 필요한 요구 사항에 맞는지 확인하십시오.|  
  
## <a name="explanation"></a>설명  
 복제를 통해 임박한 구독 만료 등의 여러 조건에 대한 이러한 경고에는 병합 게시자와 구독자 간의 변경 내용을 동기화할 때 충분한 행 수를 처리할 수 없는 오류에 대한 경고가 포함됩니다. LAN 연결과 전화 접속 연결에 대해 각각 다른 시간을 지정할 수 있습니다.  
  
 복제 모니터 또는 [sp_replmonitorchangepublicationthreshold](../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md)를 사용하여 경고를 설정할 경우 경고가 트리거되는 시기를 결정하는 임계값을 지정하십시오. 임계값에 도달하거나 임계값이 초과되면 복제 모니터에 경고가 표시되며 Windows 이벤트 로그에 이벤트가 기록됩니다. 또한 임계값에 도달하면 SQL Server 에이전트 경고가 트리거됩니다. 자세한 내용은 [복제 모니터에 임계값 및 경고 설정](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md) 및 [프로그래밍 방식으로 복제 모니터링](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)을 참조하세요.  
  
## <a name="user-action"></a>사용자 동작  
 구독이 행 처리 임계값과 일치하지 않을 경우 시스템에 성능 문제가 있는지 확인하거나 임계값 조정 여부를 확인해야 합니다. 복제를 구성한 후에는 응용 프로그램 및 토폴로지에 일반적으로 사용되는 작업과의 복제 동작 방식을 결정할 수 있는 성능 기준선을 개발하십시오. 임계값에 대한 적절한 값을 설정할 수 있도록 이 기준선에서 처리된 행의 수를 포함하십시오.  
  
 임계값이 적절하지만 초과된 경우 시스템의 성능 병목 위치를 확인해야 합니다. 복제 성능 모니터링 및 문제 해결 방법에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [복제 모니터로 성능 모니터링](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)(특히 "병합 복제에 대한 자세한 동기화 성능 보기" 섹션 참조)  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
