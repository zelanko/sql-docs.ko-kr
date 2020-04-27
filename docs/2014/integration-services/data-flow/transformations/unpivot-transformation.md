---
title: 피벗 해제 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.unpivottrans.f1
helpviewer_keywords:
- Unpivot transformation
- more normalized data set [Integration Services]
- normalized data [Integration Services]
- datasets [Integration Services], normalized data
ms.assetid: f635c64b-a9c5-4f11-9c40-9cd9d5298c5d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 98a8476ef317a0ddfa6f7fc27c0c9572ed12817a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62770200"
---
# <a name="unpivot-transformation"></a>피벗 해제 변환
  피벗 해제 변환은 단일 레코드의 여러 열 값을 단일 열에 동일 값이 포함된 여러 레코드로 확장하여 정규화되지 않은 데이터 세트를 정규화된 버전으로 만듭니다. 예를 들어 고객 이름이 나열된 데이터 세트에 각 고객마다 하나의 행이 있고 행의 열에 제품 및 구매 수량이 표시되어 있습니다. 피벗 해제 변환으로 데이터 집합을 정규화하면 데이터 집합에 고객이 구매한 각 제품이 서로 다른 행에 포함됩니다.  
  
 다음 다이어그램에서는 Product 열로 데이터를 피벗 해제하기 전의 데이터 집합을 보여 줍니다.  
  
 ![피벗 해제 후의 데이터 세트](../../media/mw-dts-18.gif "피벗 해제 후의 데이터 세트")  
  
 다음 다이어그램에서는 Product 열로 데이터를 피벗 해제한 후의 데이터 집합을 보여 줍니다.  
  
 ![피벗 해제 전의 데이터 세트](../../media/mw-dts-17.gif "피벗 해제 전의 데이터 세트")  
  
 일부 경우에는 피벗 해제된 결과에 예기치 않은 값이 있는 행이 포함될 수 있습니다. 예를 들어 다이어그램에 표시된 피벗 해제할 예제 데이터에서 Fred의 모든 Qty 열에 null 값이 있으면 출력에는 Fred에 대한 행이 다섯 개가 아니라 한 개만 포함될 수 있습니다. Qty 열에는 해당 열 데이터 형식에 따라 null이나 0이 포함됩니다.  
  
## <a name="configuration-of-the-unpivot-transformation"></a>피벗 해제 변환 구성  
 피벗 해제 변환에는 `PivotKeyValue` 사용자 지정 속성이 포함됩니다. 이 속성은 패키지가 로드되면 속성 식을 사용하여 업데이트할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](../../expressions/integration-services-ssis-expressions.md), [패키지에서 속성 식 사용](../../expressions/use-property-expressions-in-packages.md) 및 [변환 사용자 지정 속성](transformation-custom-properties.md)을 참조하세요.  
  
 이 변환은 하나의 입력과 하나의 출력을 가지며 오류 출력은 없습니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **피벗 해제 변환 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [피벗 해제 변환 편집기](../../unpivot-transformation-editor.md)  
  
 **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](../../common-properties.md)  
  
-   [Transformation Custom Properties](transformation-custom-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
  
