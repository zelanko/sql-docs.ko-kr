---
title: "게시 정보, 경고(스냅숏 게시, SQL Server 2005 이상) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.publicationinfo.warningsandagents.snapshot.f1"
ms.assetid: 7aa2eb52-b6b7-4dd3-8483-8ef00d9f0435
caps.latest.revision: 26
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# 게시 정보, 경고(스냅숏 게시, SQL Server 2005 이상)
  **경고** 탭은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전을 실행하는 배포자에서 사용할 수 있습니다. **경고** 탭을 사용하면 선택한 게시에 대해 다음 태스크를 수행할 수 있습니다.  
  
-   경고 사용  
  
-   경고와 연결된 임계값 지정  
  
-   경고와 연결된 알림 신호 정의  
  
## 경고, 임계값 및 알림 신호  
 기본적으로 복제 모니터는 초기화되지 않은 구독에 대해 경고를 표시합니다. **초기화되지 않은 구독** 상태는 구독 정보가 포함된 페이지의 **상태** 열에 경고로 표시됩니다. 스냅숏 게시의 경우 **구독이 임계값 내에 만료되는 경우 경고**옵션을 설정하여 구독의 만료가 임박하면 경고를 표시하도록 지정할 수도 있습니다. 지정된 된 임계값에 도달 하거나 초과, 구독 상태도 표시 됩니다 **곧 만료 됨/만료 됨** (하지 않는 한 우선 순위가 높은 문제가 표시).  
  
 임계값에 도달하면 복제 모니터에 경고가 표시되는 것은 물론 알림 신호가 트리거될 수 있습니다. 알림 신호는 **경고 구성** 을 클릭하고 **복제 경고 구성** 대화 상자에서 정보를 제공하여 정의합니다.  
  
## 옵션  
 **설정**  
 경고를 설정하고 임계값을 지정하려면 선택합니다.  
  
 **경고**  
 임계값과 연결된 경고에 대한 설명입니다.  
  
 **임계값**  
 임계값을 지정합니다.  
  
 **경고 구성**  
 행을 선택는 **경고** 눈금과 클릭 **경고 구성** 시작 하는 **복제 경고 구성** 대화 상자입니다. 이 대화 상자를 사용하면 선택한 임계값 및 경고와 연결된 알림 메시지를 정의할 수 있습니다.  
  
 **변경 내용 취소**  
 경고 및 임계값에 대한 모든 변경 내용을 취소하려면 클릭합니다.  
  
> [!NOTE]  
>  클릭 하면 **변경 내용 취소** 에 정의 된 경고에는 영향을 주지 않는 **복제 경고 구성** 대화 상자입니다.  
  
 **변경 내용 저장**  
 경고 및 임계값에 대한 모든 변경 내용을 저장하려면 클릭합니다.  
  
## 참고 항목  
 [복제 모니터 시작](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [정보 보기 및 게시 & #40;에 대 한 작업을 수행 합니다. 복제 모니터 & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [복제 모니터링](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  