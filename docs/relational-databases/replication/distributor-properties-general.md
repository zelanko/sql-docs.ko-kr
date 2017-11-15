---
title: "배포자 속성, 일반 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.configdistwizard.distproperties.general.f1
helpviewer_keywords: Distributor Properties dialog box
ms.assetid: ab4120ec-e524-4c0c-8b48-f2f40adb1a3b
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 64544ff33771c0718a7a22694087ffaa67928a80
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="distributor-properties-general"></a>배포자 속성, 일반
  **배포자 속성** 의 **일반** 페이지에서 배포 데이터베이스를 추가 및 삭제하고 배포 데이터베이스 속성을 설정할 수 있습니다.  
  
 배포 데이터베이스는 모든 유형의 복제에 대한 메타데이터 및 기록 데이터와 트랜잭션 복제에 대한 트랜잭션을 저장합니다. 대부분의 경우 배포 데이터베이스는 하나면 충분합니다. 그러나 여러 게시자가 단일 배포자를 사용하는 경우에는 각 게시자에 대해 배포 데이터베이스를 만들어 보십시오. 이렇게 하면 각 배포 데이터베이스를 통한 데이터 흐름이 고유하게 유지됩니다.  
  
## <a name="options"></a>옵션  
 **데이터베이스**  
 **데이터베이스** 속성 표는 배포자에 있는 배포 데이터베이스의 이름 및 보존 속성을 표시합니다. **트랜잭션 보존** 은 트랜잭션 복제에 대해 트랜잭션을 저장하는 시간입니다. 트랜잭션 보존을 배포 보존이라고도 합니다. **기록 보존** 은 모든 유형의 복제에 대해 기록 메타데이터를 저장하는 시간입니다. 배포 기간에 대한 자세한 내용은 [구독 만료 및 비활성화](../../relational-databases/replication/subscription-expiration-and-deactivation.md)를 참조하세요.  
  
 **배포 데이터베이스 속성**대화 상자를 시작하려면 **데이터베이스** 속성 표의 속성 단추 ( **...** )를 클릭합니다.  
  
 **새로 만들기**  
 새 배포 데이터베이스를 만들려면 클릭합니다.  
  
 **Delete**  
 **데이터베이스** 속성 표에서 기존 배포 데이터베이스를 선택하고 **삭제** 를 클릭하여 데이터베이스를 삭제합니다. 배포 데이터베이스가 하나만 있는 경우 배포 데이터베이스를 삭제할 수 없습니다. 각 배포자에는 배포 데이터베이스가 최소한 하나 이상 있어야 합니다. 배포 데이터베이스를 모두 삭제하려면 컴퓨터에서 배포를 해제해야 합니다. 자세한 내용은 [게시 및 배포 해제](../../relational-databases/replication/disable-publishing-and-distribution.md)를 참조하세요.  
  
 **프로필 기본값**  
 **에이전트 프로필** 대화 상자의 복제 에이전트 프로필에 액세스하려면 클릭합니다. 프로필에 대한 자세한 내용은 [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md)을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [배포 구성](../../relational-databases/replication/configure-distribution.md)   
 [배포자 및 게시자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)  
  
  
