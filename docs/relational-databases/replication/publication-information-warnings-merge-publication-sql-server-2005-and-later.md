---
title: 경고(병합 게시 정보)
description: SQL Server 2005 이상에 있는 SQL Server Management Studio 병합 복제 게시 정보 페이지의 ‘경고’ 탭을 설명합니다.
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publicationinfo.warningsandagents.merge.f1
ms.assetid: 9bef3565-5f13-42ac-8723-ebe55b0c11e6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d12b863ad925a80a3403df4861faafeddaf230d0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720917"
---
# <a name="publication-information-warnings-merge-publication-sql-server-2005-and-later"></a>게시 정보, 경고(병합 게시, SQL Server 2005 이상)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **경고** 탭은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전을 실행하는 배포자에서 사용할 수 있습니다. **경고** 탭을 사용하면 선택한 게시에 대해 다음 태스크를 수행할 수 있습니다.  
  
-   경고 사용  
  
-   경고와 연결된 임계값 지정  
  
-   경고와 연결된 알림 신호 정의  
  
## <a name="warnings-thresholds-and-alerts"></a>경고, 임계값 및 알림 신호  
 기본적으로 복제 모니터는 초기화되지 않은 구독에 대해 경고를 표시합니다. **초기화되지 않은 구독** 상태는 구독 정보가 포함된 페이지의 **상태** 열에 경고로 표시됩니다. 병합 게시의 경우 다음 추가 조건으로 인한 경고 발생 여부를 지정할 수 있습니다.  
  
-   구독 만료가 임박한 경우  
  
     이 조건은 **구독이 임계값 내에 만료되는 경우 경고**옵션에 해당합니다. 지정한 임계값에 도달하거나 이 값을 초과하면 우선 순위가 더 높은 문제가 발생하지 않는 한 구독 상태가 **곧 만료됨/만료됨** 으로 표시됩니다.  
  
-   지정된 동기화 시간이 초과된 경우  
  
     이 조건은 **전화 접속 연결 시 병합 길이가 임계값을 초과하는 경우 경고** 및 **LAN 연결 시 병합 길이가 임계값을 초과하는 경우 경고**옵션에 해당합니다. 두 임계값을 모두 설정할 수 있지만 지정한 동기화 중에는 임계값을 하나만 사용합니다. 병합 에이전트에서는 연결 유형을 기준으로 적절한 임계값을 적용합니다.  
  
     지정한 임계값에 도달하거나 이 값을 초과하면 우선 순위가 더 높은 문제가 발생하지 않는 한 구독 상태가 **장기 실행 트랜잭션 병합** 으로 표시됩니다.  
  
-   지정된 시간 내에 지정된 수의 행을 처리하지 못한 경우  
  
     이 조건은 **전화 접속 연결 시 초당 병합된 행이 임계값 미만인 경우 경고** 및 **LAN 연결 시 병합 길이가 임계값을 초과하는 경우 경고**옵션에 해당합니다. 두 임계값을 모두 설정할 수 있지만 지정한 동기화 중에는 임계값을 하나만 사용합니다. 병합 에이전트에서는 연결 유형을 기준으로 적절한 임계값을 적용합니다.  
  
     지정한 임계값에 도달하거나 이 값을 초과하면 우선 순위가 더 높은 문제가 발생하지 않는 한 구독 상태가 **성능 심각** 으로 표시됩니다.  
  
 경고를 설정할 때는 임계값도 설정해야 합니다. 예를 들어 **LAN 연결 시 병합 길이가 임계값을 초과하는 경우 경고**를 설정한 경우 병합 동기화에 대한 최대 허용 시간을 설정합니다.  
  
 임계값에 도달하면 복제 모니터에 경고가 표시되는 것은 물론 알림 신호가 트리거될 수 있습니다. 알림 신호는 **경고 구성** 을 클릭하고 **복제 경고 구성** 대화 상자에서 정보를 제공하여 정의합니다.  
  
## <a name="options"></a>옵션  
 **Enabled**  
 경고를 설정하고 임계값을 지정하려면 선택합니다.  
  
 **경고**  
 지정된 복제 경고에 대한 경고 설정을 사용하도록 설정하려면 선택합니다.  
  
 **경고**  
 임계값과 연결된 경고에 대한 설명입니다.  
  
 **임계값**  
 임계값을 지정합니다.  
  
 **경고 구성**  
 **경고** 표에서 행을 선택하고 **경고 구성** 을 클릭하여 **복제 경고 구성** 대화 상자를 시작합니다. 이 대화 상자를 사용하면 선택한 임계값 및 경고와 연결된 알림 메시지를 정의할 수 있습니다.  
  
 **변경 내용 취소**  
 경고 및 임계값에 대한 모든 변경 내용을 취소하려면 클릭합니다.  
  
> [!NOTE]  
>  **변경 내용 취소** 를 클릭해도 **복제 경고 구성** 대화 상자에서 정의한 알림 신호에는 적용되지 않습니다.  
  
 **변경 내용 저장**  
 경고 및 임계값에 대한 모든 변경 내용을 저장하려면 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 모니터 시작](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [복제 모니터를 사용하여 정보 보기 및 태스크 수행](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [복제 모니터로 성능 모니터링](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)   
 [복제 모니터링](../../relational-databases/replication/monitor/monitoring-replication.md)   
 [Set Thresholds and Warnings in Replication Monitor](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
  
  
