---
description: 구독 초기화
title: 구독 초기화 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.initializesubscriptions.f1
ms.assetid: 7b170e4e-470d-4828-a9ed-7435b0b03514
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: a813cc6483648ad47c82c4b71212ed1904c4f0ef
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463244"
---
# <a name="initialize-subscriptions"></a>구독 초기화
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  구독자는 초기화되어야만 복제된 데이터를 받을 수 있습니다. 초기 데이터 세트는 필요 없지만 구독자에는 적어도 복제된 각 개체에 대한 스키마와 복제에 필요한 메타데이터 테이블 및 프로시저가 있어야 합니다.  
  
## <a name="options"></a>옵션  
 **구독 속성**  
 초기 데이터 집합이 필요한 각 구독자의 **초기화** 열에서 확인란을 선택합니다. 확인란 선택을 취소하면 복제 메타데이터 및 프로시저만 초기화됩니다. 스냅샷 없이 구독 초기화에 대한 자세한 내용은 [스냅샷 없이 트랜잭션 구독 초기화](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)를 참조하세요.  
  
 이 마법사가 완료된 다음 병합 에이전트 또는 배포 에이전트가 스냅샷 파일을 구독자에게 전송하게 하려면 **초기화 시기** 열의 드롭다운 목록 상자에서 **즉시** 를 선택합니다. 에이전트가 다음 실행 일정에 파일을 전송하게 하려면 **첫 번째 동기화 시** 를 선택합니다. **즉시** 옵션은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]에 대한 끌어오기 구독에 사용할 수 없습니다. 병합 에이전트 및 배포 에이전트는 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]인스턴스에서 실행되지 않으므로 다른 방법으로 구독을 초기화해야 합니다.  
  
> [!NOTE]  
>  마법사에서 배포 에이전트 또는 병합 에이전트에 대해 해당 작업을 시작하려면 배포자에 연결하라는 메시지를 표시할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [구독 초기화](../../relational-databases/replication/initialize-a-subscription.md)   
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
