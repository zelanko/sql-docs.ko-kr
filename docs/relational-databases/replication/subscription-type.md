---
description: 구독 유형
title: 구독 유형 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.subscriptiontype.f1
ms.assetid: 9a50f588-ee45-4a87-826f-372ff0798587
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: cbdd0bd4a5d22c3fba7ccc7412cdc94334d01231
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468744"
---
# <a name="subscription-type"></a>구독 유형
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  병합 복제는 서버와 클라이언트라는 구독 유형을 제공합니다. 이전 버전의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 각각 전역 및 로컬이라고 불렀습니다. 서버 구독이 있는 구독자는 다음을 수행할 수 있습니다.  
  
-   데이터를 다른 구독자에 다시 게시합니다.  
  
-   대체 동기화 파트너 역할을 수행합니다.  
  
-   설정한 우선 순위에 따라 충돌을 해결합니다.  
  
 대부분의 구독자는 이 기능이 필요하지 않으며 클라이언트 구독을 사용할 수 있습니다. 클라이언트 구독을 사용하면 충돌 감지 및 해결이 가능하지만 구독자에게 우선 순위가 할당되지 않습니다. 변경 내용을 게시자에 전송할 첫 번째 구독자는 해당 변경 내용으로 인해 발생하는 모든 충돌에서 우선 적용됩니다.  
  
> [!NOTE]  
>  구독 유형은 구독을 만든 후에는 변경할 수 없습니다.  
  
## <a name="options"></a>옵션  
 **구독 속성**  
 각 구독자에 대해 **구독 유형** 열의 드롭다운 목록 상자에서 **클라이언트** 또는 **서버** 를 선택합니다. 서버 구독이 있는 구독자의 경우 **충돌 해결의 우선 순위** 열에 0에서 99.99 사이의 숫자를 입력합니다. 숫자가 클수록 구독자에 대한 우선 순위가 높습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
