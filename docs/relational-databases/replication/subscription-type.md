---
title: 구독 유형 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.subscriptiontype.f1
ms.assetid: 9a50f588-ee45-4a87-826f-372ff0798587
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c2081b616a54e7081484369627dcc42e74c95a3b
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43066749"
---
# <a name="subscription-type"></a>구독 유형
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  병합 복제는 서버와 클라이언트라는 구독 유형을 제공합니다. 이전 버전의 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 각각 전역 및 로컬이라고 불렀습니다. 서버 구독이 있는 구독자는 다음을 수행할 수 있습니다.  
  
-   데이터를 다른 구독자에 다시 게시합니다.  
  
-   대체 동기화 파트너 역할을 수행합니다.  
  
-   설정한 우선 순위에 따라 충돌을 해결합니다.  
  
 대부분의 구독자는 이 기능이 필요하지 않으며 클라이언트 구독을 사용할 수 있습니다. 클라이언트 구독을 사용하면 충돌 감지 및 해결이 가능하지만 구독자에게 우선 순위가 할당되지 않습니다. 변경 내용을 게시자에 전송할 첫 번째 구독자는 해당 변경 내용으로 인해 발생하는 모든 충돌에서 우선 적용됩니다.  
  
> [!NOTE]  
>  구독 유형은 구독을 만든 후에는 변경할 수 없습니다.  
  
## <a name="options"></a>Options  
 **구독 속성**  
 각 구독자에 대해 **구독 유형** 열의 드롭다운 목록 상자에서 **클라이언트** 또는 **서버** 를 선택합니다. 서버 구독이 있는 구독자의 경우 **충돌 해결의 우선 순위** 열에 0에서 99.99 사이의 숫자를 입력합니다. 숫자가 클수록 구독자에 대한 우선 순위가 높습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
