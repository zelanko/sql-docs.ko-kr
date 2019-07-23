---
title: 구독 다시 초기화 - 단일 구독 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.reinit.single.f1
helpviewer_keywords:
- Reinitialize Subscription(s) dialog box
ms.assetid: 9b0cf0be-d1f1-4163-a0ca-d6f095aa707e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5e0a9a86e88990fc6084b5a9d8981201c46ffd7e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046745"
---
# <a name="reinitialize-subscriptions---one-subscription"></a>구독 다시 초기화 - 단일 구독
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **구독 다시 초기화** 대화 상자를 사용하여 구독을 다시 초기화하도록 표시할 수 있습니다. 다시 초기화에는 스냅샷을 구독자에 적용하는 작업이 포함됩니다. 이 작업은 트랜잭션 게시의 구독에 대한 배포 에이전트 또는 병합 게시의 구독에 대한 병합 에이전트에서 수행합니다.  
  
## <a name="options"></a>옵션  
 **현재 스냅샷 사용**  
 다음에 배포 에이전트 또는 병합 에이전트가 실행될 때 현재 스냅샷을 구독자에 적용하려면 이 옵션을 선택합니다. 유효한 스냅샷이 없으면 이 옵션을 선택할 수 없습니다.  
  
 **새 스냅샷 사용**  
 새 스냅샷으로 구독을 다시 초기화하려면 이 옵션을 선택합니다. 스냅샷 에이전트에 의해 스냅샷이 생성된 후에만 스냅샷을 구독자에 적용할 수 있습니다. 스냅샷 에이전트가 예약 실행되도록 설정한 경우에는 예약된 다음 스냅샷 에이전트가 실행될 때까지 구독이 다시 초기화되지 않습니다.  
  
 스냅샷 에이전트를 바로 시작하려면 **지금 새 스냅샷 생성** 을 선택합니다.  
  
 **다시 초기화하기 전에 동기화되지 않은 변경 내용 업로드**  
 병합 복제에 대해서만 사용할 수 있습니다. 구독자의 데이터를 스냅샷으로 덮어쓰기 전에 보류 중인 구독 데이터베이스의 변경 내용을 업로드하려면 이 옵션을 선택합니다.  
  
 매개 변수가 있는 필터를 추가, 삭제 또는 변경할 경우 다시 초기화를 진행하는 동안에는 보류 중인 구독자의 변경 내용을 게시자로 업로드할 수 없습니다. 보류 중인 변경 내용을 업로드하려면 필터를 변경하기 전에 모든 구독을 동기화하세요.  
  
 **다시 초기화 표시**  
 구독을 다시 초기화하도록 표시하려면 클릭합니다. 유효한 스냅샷을 사용할 수 있으면 다음에 배포 에이전트 또는 병합 에이전트가 해당 구독에 대해 실행될 때 이 스냅샷이 구독자에 적용됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [구독 다시 초기화](../../relational-databases/replication/reinitialize-subscriptions.md)  
  
  
