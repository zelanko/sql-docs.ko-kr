---
title: "구독 속성 - 게시자 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.subproperties.publisher.f1"
helpviewer_keywords: 
  - "구독 속성 대화 상자"
ms.assetid: d4b2bc8b-0431-4331-8305-8992c96d0d34
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# 구독 속성 - 게시자
  게시자의 **구독 속성** 대화 상자를 사용하여 밀어넣기 구독에 대한 속성을 보고 설정할 수 있습니다. 끌어오기 구독에 대한 일부 속성도 볼 수 있지만 구독자의 **구독 속성** 대화 상자는 추가 속성을 표시하고 속성을 수정할 수 있게 해줍니다.  
  
 **구독 속성** 대화 상자의 각 속성에는 설명이 포함되어 있습니다. 속성을 클릭하면 대화 상자 아래쪽에 해당 설명이 표시됩니다. 이 항목에서는 밀어넣기 구독인 경우에만 게시자에 표시되는 여러 속성에 대한 추가 정보를 제공합니다. 속성은 다음 범주로 그룹화됩니다.  
  
-   모든 구독에 적용되는 속성  
  
-   트랜잭션 구독에 적용되는 속성  
  
-   병합 구독에 적용되는 속성  
  
 옵션이 읽기 전용으로 표시되면 구독을 만들 때만 해당 옵션을 설정할 수 있습니다. 새 구독 마법사에서 사용할 수 없는 옵션을 설정하려면 저장 프로시저를 사용하여 구독을 만듭니다. 자세한 내용은 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) 및 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)를 참조하세요.  
  
## 모든 구독에 대한 옵션  
 **보안**  
 클릭는 **에이전트 프로세스 계정** 행을 선택한 다음 속성 단추를 클릭 (**...**) 배포 에이전트 또는 병합 에이전트가 실행 되는 배포자에서 계정을 변경 합니다. 배포 에이전트 또는 병합 에이전트를 연결 하는 구독자에 게 계정을 변경 하려면 **구독자 연결**, 다음 속성 단추를 클릭 하 고 (**...**).  
  
 각 에이전트에 필요한 사용 권한에 대한 자세한 내용은 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하십시오.  
  
## 트랜잭션 구독에 대한 옵션  
 **트랜잭션 루핑 방지**  
 배포 에이전트가 구독자에서 나온 트랜잭션을 다시 구독자에 전송하는지 여부를 결정합니다. 이 옵션은 양방향 트랜잭션 복제에 사용됩니다. 자세한 내용은 [Bidirectional Transactional Replication](../../relational-databases/replication/transactional/bidirectional-transactional-replication.md)를 참조하세요.  
  
 **업데이트할 수 있는 구독**  
 구독자 변경 내용을 게시자로 다시 복제할 것인지 여부를 결정합니다. 지연 업데이트 또는 즉시 업데이트를 사용하여 변경 내용을 복제할 수 있습니다. **구독자 업데이트 방법** 은 사용할 방법을 결정합니다. 자세한 내용은 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)를 참조하세요.  
  
## 병합 구독에 대한 옵션  
 **파티션 정의(HOST_NAME)**  
 매개 변수가 있는 필터를 사용 하는 게시에 대 한 병합 복제 중 하나를 계산 두 시스템 함수 (또는 둘 다는 필터가 두 함수를 참조 하는 경우)는 데이터를 결정 하는 동기화 중: **suser_sname ()** 또는 **host_name ()**합니다. 기본적으로 **host_name ()** 있는 병합 에이전트 실행 중이지만 새 구독 마법사에서이 값을 재정의할 수는 컴퓨터의 이름을 반환 합니다. 매개 변수가 있는 필터 및 재정의 대 한 자세한 내용은 **host_name ()**, 참조 [매개 변수가 있는 행 필터](../../relational-databases/replication/merge/parameterized-row-filters.md)합니다.  
  
 **구독 유형** 및 **우선 순위**  
 구독이 클라이언트 구독인지 서버 구독인지를 표시합니다. 구독을 만든 후에는 구독 유형을 변경할 수 없습니다. 서버 구독은 데이터를 다른 구독자에 다시 게시할 수 있으며 충돌 해결을 위한 우선 순위를 할당 받을 수 있습니다.  
  
 새 구독 마법사에서 서버 구독 유형을 선택한 경우 구독자에는 충돌을 해결하는 동안 사용되는 우선 순위가 지정됩니다.  
  
 **대화형으로 충돌 해결**  
 병합 동기화를 수행하는 동안 충돌을 해결하기 위해 대화형 해결 프로그램 사용자 인터페이스를 사용할지 여부를 결정합니다. 이 인터페이스를 사용하려면 **Windows 동기화 관리자 사용** 값을 **사용**으로 설정해야 합니다. 자세한 내용은 [Interactive Conflict Resolution](../../relational-databases/replication/merge/interactive-conflict-resolution.md)을 참조하세요.  
  
## 참고 항목  
 [끌어오기 구독 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [밀어넣기 구독 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)  
  
  