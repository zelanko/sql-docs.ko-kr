---
title: 게시 정보, 경고 (트랜잭션 게시, SQL Server 2005 이상) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publicationinfo.warningsandagents.tran.f1
ms.assetid: 4d4baf1d-d0a1-4d09-bec7-137811f43f09
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 50ade30369ecdc7f5350503cc0e676a8158bb466
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061526"
---
# <a name="publication-information-warnings-transactional-publication-sql-server-2005-and-later"></a>게시 정보, 경고(트랜잭션 게시, SQL Server 2005 이상)
  **경고** 탭은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전을 실행하는 배포자에서 사용할 수 있습니다. **경고** 탭을 사용하면 선택한 게시에 대해 다음 태스크를 수행할 수 있습니다.  
  
-   복제 모니터에 경고를 표시하도록 설정  
  
-   경고와 연결된 임계값 지정  
  
-   경고와 연결된 알림 신호 정의  
  
## <a name="warnings-thresholds-and-alerts"></a>경고, 임계값 및 알림 신호  
 기본적으로 복제 모니터는 초기화되지 않은 구독에 대해 경고를 표시합니다. **초기화되지 않은 구독** 상태는 구독 정보가 포함된 페이지의 **상태** 열에 경고로 표시됩니다. 트랜잭션 게시의 경우 다음과 같은 추가 조건을 경고로 처리할 것인지 여부를 지정할 수 있습니다.  
  
-   구독 만료가 임박한 경우  
  
     이 조건은 **구독이 임계값 내에 만료되는 경우 경고**옵션에 해당합니다. 지정한 임계값에 도달하거나 이 값을 초과하면 우선 순위가 더 높은 문제가 발생하지 않는 한 구독 상태가 **곧 만료됨/만료됨** 으로 표시됩니다.  
  
-   지정한 대기 시간, 즉 게시자에서 트랜잭션이 커밋되는 시점과 구독자에서 해당 트랜잭션이 커밋되는 시점 간의 시간 간격이 초과된 경우  
  
     이 조건은 **대기 시간이 임계값을 초과하는 경우 경고**옵션에 해당합니다. 지정한 임계값에 도달하거나 이 값을 초과하면 우선 순위가 더 높은 문제가 발생하지 않는 한 구독 상태가 **성능 심각** 으로 표시됩니다. 또한 임계값은 구독 정보가 포함된 페이지의 **성능** 열에 표시되는 성능 등급을 제공하는 데 사용됩니다. 성능 등급은 다음 값 중 하나입니다.  
  
    -   우수  
  
    -   좋음  
  
    -   보통  
  
    -   나쁨  
  
    -   위험  
  
 경고를 설정할 때는 임계값도 설정해야 합니다. 예를 들어 경고 **대기 시간이 임계값을 초과하는 경우 경고**를 설정하면 게시자에서 커밋 중인 트랜잭션과 구독자에서 커밋 중인 트랜잭션 간에 허용 가능한 시간을 선택해야 합니다.  
  
 임계값에 도달하면 복제 모니터에 경고가 표시되는 것은 물론 알림 신호가 트리거될 수 있습니다. 알림 신호는 **경고 구성** 을 클릭하고 **복제 경고 구성** 대화 상자에서 정보를 제공하여 정의합니다.  
  
## <a name="options"></a>옵션  
 **Enabled**  
 경고를 설정하고 임계값을 지정하려면 선택합니다.  
  
 **Warning**  
 임계값과 연결된 경고에 대한 설명입니다.  
  
 **고대비**  
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
 [복제 모니터 시작](monitor/start-the-replication-monitor.md)   
 [복제 모니터를 사용 하 여 정보 보기 및 태스크 수행](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [복제 모니터를 사용 하 여 성능 모니터링](monitor/monitor-performance-with-replication-monitor.md)   
 [복제 모니터링](monitoring-replication.md)   
 [Set Thresholds and Warnings in Replication Monitor](monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
  
  
