---
title: "대화형 충돌 해결 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "대화형 충돌 해결 [SQL Server 복제]"
  - "대화형 해결 프로그램 [SQL Server 복제]"
  - "아티클 [SQL Server 복제], 충돌 해결"
  - "충돌 해결 [SQL Server 복제], 병합 복제"
ms.assetid: 172c60c7-f605-4eb5-b185-54ae9e9d3c60
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 대화형 충돌 해결
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 요청 시 동기화 중 충돌을 수동으로 해결할 수 있는 대화형 해결 프로그램을 제공 하는 복제 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 동기화 관리자입니다. 런타임 시 활성화되는 대화형 해결 프로그램은 충돌하는 각 행의 데이터를 표시하여 충돌 데이터를 보고 편집하며 각 충돌을 개별적으로 해결하는 옵션을 제공하는 그래픽 인터페이스입니다.  
  
 대화형 해결 프로그램은 충돌 뷰어와 비슷합니다. 그러나 충돌 뷰어는 병합 동기화 후 이미 해결된 충돌의 결과를 표시하는 반면 대화형 해결 프로그램은 해결 전 각 충돌을 표시하여 병합 동기화 중 각 충돌의 결과를 결정하도록 허용합니다. 사용자는 충돌 발생 시 대화형 해결 프로그램을 모니터링할 수 있어야 합니다.  
  
> [!NOTE]  
>  대화형 해결을 사용하려면 Windows 동기화 관리자가 필요합니다. 동기화가 Windows 동기화 관리자 외부(예: [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 또는 복제 모니터의 예약 동기화 또는 요청 시 동기화)에서 수행된 경우 아티클에 지정된 해결 프로그램에 따라 사용자 개입 없이도 자동으로 충돌이 해결됩니다. 논리적 레코드와 관련된 충돌은 대화형 해결 프로그램에 표시되지 않습니다. 이러한 충돌에 대한 정보를 보려면 복제 저장 프로시저를 사용합니다. 자세한 내용은 참조 [병합 게시 및 #40;에 대 한 충돌 정보 보기 복제 TRANSACT-SQL 프로그래밍 & #41;](../../../relational-databases/replication/view conflict information for merge publications.md)합니다.  
  
## 아티클 해결 프로그램 및 대화형 해결 프로그램  
 게시가 만들어질 때 충돌 해결 프로그램(기본 해결 프로그램, 비즈니스 논리 처리기 또는 사용자 지정 해결 프로그램)은 특정 아티클에 할당되며 규칙 집합을 사용하여 충돌하는 행 데이터 입력 시 사용해야 하는 데이터 집합을 결정합니다. 대화형 해결 프로그램은 충돌 시 적용되는 내용과 삭제되는 내용을 결정하는 규칙을 가진 별도의 충돌 해결 프로그램이 아니라 기본 및 사용자 지정 해결 프로그램과 함께 사용되는 도구입니다. 아티클 해결 프로그램도 적용할 행 및 삭제할 행을 결정하지만 대화형 해결 프로그램으로 사용자는 결과를 승인, 거부 또는 수정할 수 있는 간섭 기능을 가집니다.  
  
 대화형 해결 프로그램을 사용하려면 필요한 각 아티클과 구독에 대해 대화형 해결을 사용할 수 있게 설정해야 합니다. 하나 이상의 아티클과 구독에 대해 대화형 해결을 사용할 수 있게 설정하면 병합 동기화 중 충돌이 감지될 때 대화형 해결 프로그램이 사용됩니다.  
  
 대화형 해결 프로그램을 사용 하려면 참조 [병합 아티클에 대 한 대화형 충돌 해결 지정](../../../relational-databases/replication/publish/specify-interactive-conflict-resolution-for-merge-articles.md) 및 [는 구독 사용 하 여 Windows 동기화 관리자 & #40; 동기화 Windows 동기화 관리자 & #41;](../../../relational-databases/replication/synchronize a subscription using windows synchronization manager.md)합니다.  
  
## 참고 항목  
 [고급 병합 복제 충돌 감지 및 해결](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  