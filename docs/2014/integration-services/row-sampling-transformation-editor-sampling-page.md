---
title: 행 샘플링 변환 편집기 (샘플링 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.ROWSAMPLINGTRANSFORMATION.COLUMNS.F1
- sql12.dts.designer.rowsamplingtransformation.f1
helpviewer_keywords:
- Row Sampling Transformation Editor
ms.assetid: 544c7709-6de0-4c08-bda3-759985be9a05
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 30163b4d65ac6a732efb3f7c67a018f433a42ac0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66056453"
---
# <a name="row-sampling-transformation-editor-sampling-page"></a>행 샘플링 변환 편집기(샘플링 페이지)
  **행 샘플링 변환 편집기** 대화 상자를 사용하여 입력의 일부분을 지정된 행 수를 사용하는 샘플로 분할할 수 있습니다. 이 변환으로 인해 입력이 두 개의 별도 출력으로 나뉩니다.  
  
 행 샘플링 변환에 대한 자세한 내용은 [Row Sampling Transformation](data-flow/transformations/row-sampling-transformation.md)을 참조하십시오.  
  
## <a name="options"></a>옵션  
 **행 수**  
 입력에서 샘플로 사용할 행 수를 지정합니다.  
  
 이 속성의 값은 속성 식을 사용하여 지정할 수 있습니다.  
  
 **샘플 출력 이름**  
 샘플링한 행이 포함될 출력에 사용할 고유 이름을 제공합니다. 제공한 이름은 SSIS 디자이너에 표시됩니다.  
  
 **선택하지 않은 출력 이름**  
 샘플링에서 제외된 행이 포함될 출력에 사용할 고유 이름을 제공합니다. 제공한 이름은 SSIS 디자이너에 표시됩니다.  
  
 **다음과 같은 임의 초기값 사용**  
 변환에서 샘플을 만드는 데 사용하는 난수 생성기에 샘플링 초기값을 지정합니다. 이 옵션은 개발 및 테스트 용도로만 사용하는 것이 좋습니다. 임의 초기값을 지정하지 않으면 변환에서 Microsoft Windows 틱 수를 초기값으로 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [비율 샘플링 변환](data-flow/transformations/percentage-sampling-transformation.md)  
  
  
