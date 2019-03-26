---
title: 고정 및 변경 특성 옵션(느린 변경 차원 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.loaddimwizard.attriboption.f1
ms.assetid: c841345c-7d03-452f-9379-1c8c464f029c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5057ade3b02e3d6b4348ec1a199da07920a4ced4
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58273938"
---
# <a name="fixed-and-changing-attribute-options-slowly-changing-dimension-wizard"></a>고정 및 변경 특성 옵션(느린 변경 차원 마법사)
  **고정 및 변경 특성 옵션** 대화 상자를 사용하여 고정 및 변경 특성에서 변경 작업에 대응하는 방법을 지정할 수 있습니다.  
  
 이 마법사에 대한 자세한 내용은 [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)를 참조하십시오.  
  
## <a name="options"></a>옵션  
 **고정 특성**  
 고정 특성에서 변경이 감지된 경우 태스크를 실패한 것으로 처리할지 여부를 나타냅니다.  
  
 **변경 특성**  
 변경 특성에서 변경이 감지된 경우 태스크 결과로 현재 레코드와 함께 오래된 레코드나 만료된 레코드를 변경할지 여부를 나타냅니다. 만료된 레코드란 유형 2 변경과 같이 기록 특성이 변경되어 새 레코드로 바뀐 레코드를 말합니다. 이 옵션을 선택하면 관계형 데이터 웨어하우스에 생성된 다차원 개체의 추가 처리 요구 사항을 설정할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [느린 변경 차원 마법사를 사용하여 출력 구성](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
