---
title: 배포 보존 기간 설정
description: SSMS(SQL Server Management Studio)에서 배포 데이터베이스 내의 데이터에 대한 보존 기간을 설정합니다.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transaction retention periods [SQL Server replication]
- retention periods [SQL Server replication]
ms.assetid: 9a98c53a-fea5-4235-b23d-6c69587c5676
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: a5f1f925d4ab0438ab237a903b2ad80007e86e20
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479734"
---
# <a name="set-distribution-retention-period-for-transactional-publications"></a>트랜잭션 게시에 대한 배포 보존 기간 설정
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  **배포 데이터베이스 속성 - \<DistributionDatabase>** 대화 상자에서 최소 배포 보존 기간과 최대 배포 보존 기간을 지정합니다. 이는 **배포자 속성 - \<Distributor>** 대화 상자의 **일반** 페이지에서 사용할 수 있습니다. 이 대화 상자에 액세스하는 방법은 [배포자 및 게시자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)을 참조하세요.  
  
### <a name="to-specify-the-distribution-retention-period"></a>배포 보존 기간을 지정하려면  
  
1.  **배포자 속성 - \<Distributor>** 대화 상자의 **일반** 페이지에서 배포 데이터베이스의 속성 단추( **...** )를 클릭합니다.  
  
2.  최소 배포 보존 기간을 지정하려면 **최소** 상자에 값을 입력하고, 최대 배포 보존 기간을 지정하려면 **최대** 상자에 값을 입력합니다.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="see-also"></a>참고 항목  
 [배포 구성](../../relational-databases/replication/configure-distribution.md)   
 [구독 만료 및 비활성화](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
