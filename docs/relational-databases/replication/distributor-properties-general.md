---
title: "배포자 속성, 일반 | Microsoft Docs"
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
  - "sql13.rep.configdistwizard.distproperties.general.f1"
helpviewer_keywords: 
  - "배포자 속성 대화 상자"
ms.assetid: ab4120ec-e524-4c0c-8b48-f2f40adb1a3b
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# 배포자 속성, 일반
  **배포자 속성** 의 **일반** 페이지에서 배포 데이터베이스를 추가 및 삭제하고 배포 데이터베이스 속성을 설정할 수 있습니다.  
  
 배포 데이터베이스는 모든 유형의 복제에 대한 메타데이터 및 기록 데이터와 트랜잭션 복제에 대한 트랜잭션을 저장합니다. 대부분의 경우 배포 데이터베이스는 하나면 충분합니다. 그러나 여러 게시자가 단일 배포자를 사용하는 경우에는 각 게시자에 대해 배포 데이터베이스를 만들어 보십시오. 이렇게 하면 각 배포 데이터베이스를 통한 데이터 흐름이 고유하게 유지됩니다.  
  
## 옵션  
 **데이터베이스**  
  **데이터베이스** 속성 표는 배포자에서 배포 데이터베이스의 이름 및 보존 속성을 보여 줍니다. **트랜잭션 보존** 은 트랜잭션 복제에 대 한 저장 된 시간 트랜잭션 (트랜잭션 보존 라고도 배포 보존 기간). **기록 보존** 은 모든 유형의 복제에 대해 기록 메타데이터를 저장하는 시간입니다. 배포 보존 기간에 대 한 자세한 내용은 참조 [구독 만료 및 비활성화](../../relational-databases/replication/subscription-expiration-and-deactivation.md)합니다.  
  
 속성 단추를 클릭 (**...**)에 **데이터베이스** 를 시작 하려면 속성 표는 **배포 데이터베이스 속성** 대화 상자입니다.  
  
 **새로 만들기**  
 새 배포 데이터베이스를 만들려면 클릭합니다.  
  
 **Delete**  
 기존 배포 데이터베이스를 선택 합니다.는 **데이터베이스** 속성 표 및 클릭 **삭제** 데이터베이스를 삭제 하려고 합니다. 배포 데이터베이스가 하나만 있는 경우 배포 데이터베이스를 삭제할 수 없습니다. 각 배포자에는 배포 데이터베이스가 최소한 하나 이상 있어야 합니다. 배포 데이터베이스를 모두 삭제하려면 컴퓨터에서 배포를 해제해야 합니다. 자세한 내용은 참조 [게시 및 배포 해제](../../relational-databases/replication/disable-publishing-and-distribution.md)합니다.  
  
 **프로필 기본값**  
 클릭 하 여 복제 에이전트 프로필에 대 한 액세스는 **에이전트 프로필** 대화 상자입니다. 프로필에 대한 자세한 내용은 [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md)을 참조하십시오.  
  
## 참고 항목  
 [배포 구성](../../relational-databases/replication/configure-distribution.md)   
 [게시자 및 배포자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)  
  
  