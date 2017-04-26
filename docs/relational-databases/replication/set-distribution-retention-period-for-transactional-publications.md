---
title: "트랜잭션 게시에 대한 배포 보존 기간 설정 | Microsoft 문서"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transaction retention periods [SQL Server replication]
- retention periods [SQL Server replication]
ms.assetid: 9a98c53a-fea5-4235-b23d-6c69587c5676
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1e4607ac57dec886ce1a05527daf6ab1e2dd2828
ms.lasthandoff: 04/11/2017

---
# <a name="set-distribution-retention-period-for-transactional-publications"></a>트랜잭션 게시에 대한 배포 보존 기간 설정
  **배포 데이터베이스 속성 - \<DistributionDatabase>** 대화 상자에서 최소 배포 보존 기간과 최대 배포 보존 기간을 지정합니다. **배포자 속성 - \<Distributor>** 대화 상자의 **일반** 페이지에서 사용할 수 있습니다. 이 대화 상자에 액세스하는 방법은 [배포자 및 게시자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)을 참조하세요.  
  
### <a name="to-specify-the-distribution-retention-period"></a>배포 보존 기간을 지정하려면  
  
1.  **배포자 속성 - \<Distributor>** 대화 상자의 **일반** 페이지에서 배포 데이터베이스에 대한 속성 단추(**…**)를 클릭합니다.  
  
2.  최소 배포 보존 기간을 지정하려면 **최소** 상자에 값을 입력하고, 최대 배포 보존 기간을 지정하려면 **최대** 상자에 값을 입력합니다.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목:  
 [배포 구성](../../relational-databases/replication/configure-distribution.md)   
 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
