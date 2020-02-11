---
title: 구독 유효성 검사 옵션(병합 구독) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.validate.mergeoptions.f1
helpviewer_keywords:
- Subscription Validation Options dialog box
ms.assetid: 4958c4ab-2025-42ce-b836-6fb4e9e6f24d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7d7631df4a1e4c6ec37effbc06b6a141b0d41ebc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63249291"
---
# <a name="subscription-validation-options-merge-subscriptions"></a>구독 유효성 검사 옵션(병합 구독)
  **구독 유효성 검사 옵션** 대화 상자를 사용하여 유효성 검사에서 행 개수만 사용할지, 아니면 행 개수와 이진 체크섬을 사용할지를 지정할 수 있습니다.  
  
## <a name="options"></a>옵션  
 **행 개수만 확인**  
 구독자의 테이블 행 개수가 게시자의 테이블 행 개수와 같은지 확인하려면 선택합니다. 이 방법은 행 내용이 일치하는지 여부는 확인하지 않습니다. 행 개수 유효성 검사에서는 최소 수준의 데이터 문제 인식을 위한 검사만 수행됩니다.  
  
 **행 개수를 확인하고 체크섬을 비교하여 행 데이터 확인**  
 게시자 및 구독자에서 행 개수를 확인하고 이진 체크섬 알고리즘을 사용하여 모든 데이터의 체크섬을 계산합니다. 행 개수 확인을 실패하면 체크섬 계산이 수행되지 않습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)]에는 이 옵션이 유효하지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [구독자에서 데이터 유효성 검사](validate-data-at-the-subscriber.md)   
 [복제된 데이터의 유효성 검사](validate-data-at-the-subscriber.md)  
  
  
