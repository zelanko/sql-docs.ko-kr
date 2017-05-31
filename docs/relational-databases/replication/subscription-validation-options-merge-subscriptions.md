---
title: "구독 유효성 검사 옵션(병합 구독) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.validate.mergeoptions.f1
helpviewer_keywords:
- Subscription Validation Options dialog box
ms.assetid: 4958c4ab-2025-42ce-b836-6fb4e9e6f24d
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f946728b0512ac4db66a3b6abb1182a0ac8706fa
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="subscription-validation-options-merge-subscriptions"></a>구독 유효성 검사 옵션(병합 구독)
  **구독 유효성 검사 옵션** 대화 상자를 사용하여 유효성 검사에서 행 개수만 사용할지, 아니면 행 개수와 이진 체크섬을 사용할지를 지정할 수 있습니다.  
  
## <a name="options"></a>옵션  
 **행 개수만 확인**  
 구독자의 테이블 행 개수가 게시자의 테이블 행 개수와 같은지 확인하려면 선택합니다. 이 방법은 행 내용이 일치하는지 여부는 확인하지 않습니다. 행 개수 유효성 검사에서는 최소 수준의 데이터 문제 인식을 위한 검사만 수행됩니다.  
  
 **행 개수를 확인하고 체크섬을 비교하여 행 데이터 확인**  
 게시자 및 구독자에서 행 개수를 확인하고 이진 체크섬 알고리즘을 사용하여 모든 데이터의 체크섬을 계산합니다. 행 개수 확인을 실패하면 체크섬 계산이 수행되지 않습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)]에는 이 옵션이 유효하지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [구독자에서 데이터 유효성 검사](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [복제된 데이터의 유효성 검사](../../relational-databases/replication/validate-replicated-data.md)  
  
  
