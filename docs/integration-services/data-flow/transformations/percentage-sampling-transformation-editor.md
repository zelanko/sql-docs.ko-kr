---
title: "비율 샘플링 변환 편집기 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.percentagesamplingtransformation.f1
helpviewer_keywords:
- Percentage Sampling Transformation Editor
ms.assetid: 2c40d804-26a3-4d35-809b-bc923d83d451
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a3cf0dd802330585e50428b3301270930b31766d
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="percentage-sampling-transformation-editor"></a>비율 샘플링 변환 편집기
  **비율 샘플링 변환 편집기** 대화 상자에서 지정한 행의 백분율을 사용하여 입력 부분을 샘플로 분할할 수 있습니다. 이 변환으로 인해 입력이 두 개의 별도 출력으로 나뉩니다.  
  
 비율 샘플링 변환에 대한 자세한 내용은 [Percentage Sampling Transformation](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)을 참조하십시오.  
  
## <a name="options"></a>옵션  
 **행의 백분율**  
 입력에서 샘플로 사용할 행의 백분율을 지정합니다.  
  
 이 속성의 값은 속성 식을 사용하여 지정할 수 있습니다.  
  
 **샘플 출력 이름**  
 샘플링한 행이 포함될 출력에 사용할 고유 이름을 제공합니다. 제공한 이름은 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에 표시됩니다.  
  
 **선택하지 않은 출력 이름**  
 샘플링에서 제외된 행이 포함될 출력에 사용할 고유 이름을 제공합니다. 제공한 이름은 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에 표시됩니다.  
  
 **다음과 같은 임의 초기값 사용**  
 변환에서 샘플을 만드는 데 사용하는 난수 생성기에 샘플링 초기값을 지정합니다. 이 옵션은 개발 및 테스트 용도로만 사용하는 것이 좋습니다. 임의 초기값을 지정하지 않으면 Microsoft Windows 틱 수가 사용됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services 오류 및 메시지 참조](../../../integration-services/integration-services-error-and-message-reference.md)   
 [행 샘플링 변환](../../../integration-services/data-flow/transformations/row-sampling-transformation.md)  
  
  
