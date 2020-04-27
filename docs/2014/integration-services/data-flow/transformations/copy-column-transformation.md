---
title: 열 복사 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.copycolumntrans.f1
helpviewer_keywords:
- columns [Integration Services], copying
- copying columns
- Copy Column transformation
ms.assetid: 1c72a313-9026-46bc-a57f-c6b3f47346f8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7ebdcc68c4fe8c4782251e2f4e5896e4557e23e6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62770329"
---
# <a name="copy-column-transformation"></a>열 복사 변환
  열 복사 변환은 입력 열을 복사하고 새 열을 변환 출력에 추가하여 새 열을 만듭니다. 데이터 흐름의 뒷부분에서 열 복사본에 다른 변환을 적용할 수 있습니다. 예를 들어 열 복사 변환을 사용하여 열 복사본을 만든 다음 문자표 변환을 사용하여 복사한 데이터를 대문자로 변환하거나 집계 변환을 사용하여 새 열에 집계를 적용할 수 있습니다.  
  
## <a name="configuration-of-the-copy-column-transformation"></a>열 복사 변환 구성  
 복사할 입력 열을 지정하여 열 복사 변환을 구성합니다. 특정 열의 여러 복사본이나 여러 열의 복사본을 단일 작업으로 만들 수 있습니다.  
  
 이 변환은 하나의 입력과 하나의 출력을 가지며 오류 출력은 지원하지 않습니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **열 복사 변환 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용은 [Copy Column Transformation Editor](../../copy-column-transformation-editor.md)를 참조하십시오.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](../../common-properties.md)  
  
-   [Transformation Custom Properties](transformation-custom-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 흐름](../data-flow.md)   
 [Integration Services 변환](integration-services-transformations.md)  
  
  
