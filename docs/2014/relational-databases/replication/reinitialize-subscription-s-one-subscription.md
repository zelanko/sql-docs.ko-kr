---
title: 구독 다시 초기화 - 단일 구독 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rep.reinit.single.f1
helpviewer_keywords:
- Reinitialize Subscription(s) dialog box
ms.assetid: 9b0cf0be-d1f1-4163-a0ca-d6f095aa707e
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: fa3c4afcdcf50bc34dd9fd507cea0420277ff2b2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092832"
---
# <a name="reinitialize-subscriptions---one-subscription"></a>구독 다시 초기화 - 단일 구독
  **구독 다시 초기화** 대화 상자를 사용하여 구독을 다시 초기화하도록 표시할 수 있습니다. 다시 초기화에는 스냅숏을 구독자에 적용하는 작업이 포함됩니다. 이 작업은 트랜잭션 게시의 구독에 대한 배포 에이전트 또는 병합 게시의 구독에 대한 병합 에이전트에서 수행합니다.  
  
## <a name="options"></a>변수  
 **현재 스냅숏 사용**  
 다음에 배포 에이전트 또는 병합 에이전트가 실행될 때 현재 스냅숏을 구독자에 적용하려면 이 옵션을 선택합니다. 유효한 스냅숏이 없으면 이 옵션을 선택할 수 없습니다.  
  
 **새 스냅숏 사용**  
 새 스냅숏으로 구독을 다시 초기화하려면 이 옵션을 선택합니다. 스냅숏 에이전트에 의해 스냅숏이 생성된 후에만 스냅숏을 구독자에 적용할 수 있습니다. 스냅숏 에이전트가 예약 실행되도록 설정한 경우에는 예약된 다음 스냅숏 에이전트가 실행될 때까지 구독이 다시 초기화되지 않습니다.  
  
 스냅숏 에이전트를 바로 시작하려면 **지금 새 스냅숏 생성** 을 선택합니다.  
  
 **다시 초기화하기 전에 동기화되지 않은 변경 내용 업로드**  
 병합 복제에 대해서만 사용할 수 있습니다. 구독자의 데이터를 스냅숏으로 덮어쓰기 전에 보류 중인 구독 데이터베이스의 변경 내용을 업로드하려면 이 옵션을 선택합니다.  
  
 매개 변수가 있는 필터를 추가, 삭제 또는 변경할 경우 다시 초기화를 진행하는 동안에는 보류 중인 구독자의 변경 내용을 게시자로 업로드할 수 없습니다. 보류 중인 변경 내용을 업로드하려면 필터를 변경하기 전에 모든 구독을 동기화하세요.  
  
 **다시 초기화 표시**  
 구독을 다시 초기화하도록 표시하려면 클릭합니다. 유효한 스냅숏을 사용할 수 있으면 다음에 배포 에이전트 또는 병합 에이전트가 해당 구독에 대해 실행될 때 이 스냅숏이 구독자에 적용됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [구독 다시 초기화](reinitialize-subscriptions.md)  
  
  