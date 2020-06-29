---
title: 멀티캐스트 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.multicasttrans.f1
helpviewer_keywords:
- multiple outputs
- Multicast transformation
- datasets [Integration Services], multiple outputs
- multiple transformations
ms.assetid: 32194784-1684-40cd-9f91-1aba4d8360d3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7b5c0a38c966c89f426a213f302b45c390b77cfe
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437610"
---
# <a name="multicast-transformation"></a>멀티캐스트 변환
  멀티캐스트 변환은 입력을 하나 이상의 출력으로 배포합니다. 이 변환은 조건부 분할 변환과 유사합니다. 둘 다 입력을 여러 출력으로 보냅니다. 두 변환의 차이점은 멀티캐스트 변환은 모든 행을 모든 출력으로 보내고 조건부 분할은 한 행을 단일 출력으로 보낸다는 것입니다. 자세한 내용은 [Conditional Split Transformation](conditional-split-transformation.md)을 참조하세요.  
  
 출력을 추가하여 멀티캐스트 변환을 구성합니다.  
  
 패키지는 멀티캐스트 변환을 사용하여 데이터의 논리적 복사본을 만들 수 있습니다. 이 기능은 패키지가 동일한 데이터에 여러 변환 집합을 적용해야 하는 경우에 유용합니다. 예를 들어 하나의 데이터 복사본이 집계되고 요약 정보만 대상에 로드되지만 대상에 로드되기 전에 조회 값과 파생 열을 사용하여 다른 데이터 복사본이 확장됩니다.  
  
 이 변환은 하나의 입력과 여러 출력을 가지며 오류 출력은 지원하지 않습니다.  
  
## <a name="configuration-of-the-multicast-transformation"></a>멀티캐스트 변환 구성  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **멀티캐스트 변환 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용은 [Multicast Transformation Editor](../../multicast-transformation-editor.md)를 참조하십시오.  
  
 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용은 [Common Properties](../../common-properties.md)을 참조하십시오.  
  
## <a name="related-tasks"></a>관련 작업  
 이 구성 요소의 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 흐름](../data-flow.md)   
 [Integration Services 변환](integration-services-transformations.md)  
  
  
