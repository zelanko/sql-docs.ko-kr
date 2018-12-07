---
title: 배포 데이터베이스 속성 | Microsoft 문서
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.configdistwizard.distdbproperties.f1
helpviewer_keywords:
- Distribution Database Properties dialog box
ms.assetid: 0f404ab9-1237-4936-8df5-888baab6a245
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5d833e97138dd184f35378ad39f96a9f71675d67
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52535827"
---
# <a name="distribution-database-properties"></a>배포 데이터베이스 속성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **배포 데이터베이스 속성** 대화 상자를 사용하여 많은 속성을 보고 데이터베이스의 트랜잭션 보존 기간과 기록 보존 기간을 설정할 수 있습니다.  
  
## <a name="options"></a>Options  
 **이름**  
 배포 데이터베이스의 이름으로 기본값은 'distribution'입니다(읽기 전용).  
  
 **파일 위치**  
 데이터베이스 파일과 로그 파일의 위치입니다(읽기 전용).  
  
 **트랜잭션 보존 기간**  
 배포 보존 기간이라고도 합니다. 트랜잭션 복제에서 트랜잭션이 저장되는 시간입니다. 자세한 내용은 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)을(를) 참조하세요.  
  
 **기록 보존 기간**  
 모든 복제 유형에서 기록 메타데이터가 저장되는 시간입니다.  
  
 **큐 판독기 에이전트 보안**  
 큐 판독기 에이전트는 지연 업데이트 구독이 있는 트랜잭션 복제에서 사용합니다. 새 게시 마법사의 **게시 유형** 페이지에서 **업데이트할 수 있는 구독이 있는 트랜잭션 게시** 를 선택하면 큐 판독기 에이전트가 자동으로 생성됩니다. **보안 설정...** 을 클릭하여 에이전트를 실행하고 배포자에 연결되는 계정을 변경합니다.  
  
 이 페이지에서 **큐 판독기 에이전트 만들기** 를 선택하여 큐 판독기 에이전트를 만들 수도 있습니다. 에이전트가 이미 생성된 경우에는 이 옵션을 사용할 수 없습니다.  
  
 큐 판독기 에이전트에 대한 추가 연결 정보는 다음 두 위치에서 지정합니다.  
  
-   에이전트는 **게시자 속성** 대화 상자에서 지정한 자격 증명을 사용하여 게시자에 연결합니다. 이 대화 상자는 **배포자 속성** 대화 상자의 **게시자** 페이지에서 사용할 수 있습니다.  
  
-   에이전트는 새 구독 마법사에서 배포 에이전트에 대해 지정된 자격 증명을 사용하여 구독자에 연결합니다.  
  
 자세한 내용은  [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [배포 구성](../../relational-databases/replication/configure-distribution.md)   
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [배포자 및 게시자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)  
  
  
