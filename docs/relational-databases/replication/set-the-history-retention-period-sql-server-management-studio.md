---
title: 기록 보존 기간 설정(SSMS)
description: SSMS(SQL Server Management Studio)에서 배포 데이터베이스 기록 보존 기간을 설정하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- history retention periods [SQL Server replication]
- retention periods [SQL Server replication]
ms.assetid: c288daab-5181-4d4b-ba2a-8a147098e758
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 6f9ada00c3166637ca1c5721b17ed950df58a4e2
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76287200"
---
# <a name="set-the-history-retention-period-sql-server-management-studio"></a>기록 보존 기간 설정(SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  **배포 데이터베이스 속성 - \<DistributionDatabase>** 대화 상자의 **일반** 페이지에서 기록 보존 기간을 지정합니다. 이 설정은 복제 에이전트 기록이 저장되는 기간을 제어합니다. **배포자 속성 - \<Distributor>** 대화 상자의 **일반** 페이지에서 이 페이지를 사용할 수 있습니다. 이 대화 상자에 액세스하는 방법은 [배포자 및 게시자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)을 참조하세요.  
  
### <a name="to-specify-the-history-retention-period"></a>기록 보존 기간을 지정하려면  
  
1.  **배포자 속성 - \<Distributor>** 대화 상자의 **일반** 페이지에서 배포 데이터베이스에 대한 속성 단추(**…**)를 클릭합니다.  
  
2.  **최소 다음 기간 동안 복제 성능 기록 저장** 상자에 값을 입력합니다.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [배포 구성](../../relational-databases/replication/configure-distribution.md)  
  
  
