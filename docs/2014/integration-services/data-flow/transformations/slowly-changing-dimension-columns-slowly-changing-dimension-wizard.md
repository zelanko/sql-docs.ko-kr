---
title: 느린 변경 차원 열(느린 변경 차원 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.loaddimwizard.scdsupport.f1
ms.assetid: 36de99d5-5368-48e0-b876-17e9c6862c6c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c49f0ce7498215d5758557fba4c67740dca1239e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62770674"
---
# <a name="slowly-changing-dimension-columns-slowly-changing-dimension-wizard"></a>느린 변경 차원 열(느린 변경 차원 마법사)
  **느린 변경 차원 열** 대화 상자를 사용하여 각 느린 변경 차원 열의 변경 유형을 선택할 수 있습니다.  
  
 이 마법사에 대한 자세한 내용은 [Slowly Changing Dimension Transformation](slowly-changing-dimension-transformation.md)를 참조하십시오.  
  
## <a name="options"></a>변수  
 **차원 열**  
 목록에서 차원 열을 선택합니다.  
  
 **변경 유형**  
 **고정 특성**을 선택하거나 두 변경 특성 유형 중 하나를 선택합니다. 열 값이 변경되지 않을 경우에는 **고정 특성** 을 사용합니다. 이렇게 하면 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 에서 변경 내용을 오류로 처리합니다. 변경된 값으로 기존 값을 덮어쓰려면 **변경 특성** 을 사용합니다. 변경된 값을 새 레코드에 저장하고 이전 레코드는 오래된 레코드로 표시하려면 **기록 특성** 을 사용합니다.  
  
 **제거**  
 매핑된 열 목록에서 차원 열을 제거하려면 열을 선택한 후 **제거**를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [느린 변경 차원 마법사를 사용하여 출력 구성](configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
