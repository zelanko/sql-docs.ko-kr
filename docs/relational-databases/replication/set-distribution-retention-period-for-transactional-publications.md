---
title: "트랜잭션 게시에 대한 배포 보존 기간 설정 | Microsoft 문서"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transaction retention periods [SQL Server replication]
- retention periods [SQL Server replication]
ms.assetid: 9a98c53a-fea5-4235-b23d-6c69587c5676
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3a4c7ebac3ab29e62d633f03891014f6088f2711
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="set-distribution-retention-period-for-transactional-publications"></a>트랜잭션 게시에 대한 배포 보존 기간 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **배포 데이터베이스 속성 - \<DistributionDatabase>** 대화 상자에서 최소 배포 보존 기간과 최대 배포 보존 기간을 지정합니다. **배포자 속성 - \<Distributor>** 대화 상자의 **일반** 페이지에서 사용할 수 있습니다. 이 대화 상자에 액세스하는 방법은 [배포자 및 게시자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)을 참조하세요.  
  
### <a name="to-specify-the-distribution-retention-period"></a>배포 보존 기간을 지정하려면  
  
1.  **배포자 속성 - \<Distributor>** 대화 상자의 **일반** 페이지에서 배포 데이터베이스에 대한 속성 단추(**…**)를 클릭합니다.  
  
2.  최소 배포 보존 기간을 지정하려면 **최소** 상자에 값을 입력하고, 최대 배포 보존 기간을 지정하려면 **최대** 상자에 값을 입력합니다.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [배포 구성](../../relational-databases/replication/configure-distribution.md)   
 [구독 만료 및 비활성화](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
