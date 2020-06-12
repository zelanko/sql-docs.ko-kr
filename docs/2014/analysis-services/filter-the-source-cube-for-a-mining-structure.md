---
title: 마이닝 구조에 대 한 원본 큐브 필터링 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- slice cubes [Analysis Services]
- mining structures [Analysis Services], filtering source cube
- cubes [Analysis Services], slicing
- filtering data [Analysis Services]
ms.assetid: 05dce7e1-2fe5-4500-bacf-c1a8a76e1424
author: minewiskan
ms.author: owend
ms.openlocfilehash: 058ba6e78fd6c6e5aa7b06fbd5d34c256dac07b3
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544455"
---
# <a name="filter-the-source-cube-for-a-mining-structure"></a>마이닝 구조에 대한 원본 큐브 필터링
  다차원 모델 (OLAP 큐브)의 데이터를 기반으로 하는 마이닝 구조를 만드는 경우 마이닝 구조의 기반이 되는 큐브를 *분할할* 수 있습니다. 조각화하면 마이닝 모델 학습에 사용되는 데이터에 대한 일종의 필터로 데이터 하위 집합을 만들 수 있습니다.  
  
### <a name="to-slice-a-cube"></a>큐브를 조각화하려면  
  
1.  의 데이터 마이닝 디자이너에서 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] **마이닝 구조** 탭 이나 **마이닝 모델** 탭을 선택 합니다.  
  
2.  **마이닝 모델** 메뉴에서 **마이닝 구조 큐브 조각 정의**를 선택 합니다.  
  
     **큐브 조각화** 대화 상자가 열립니다.  
  
3.  **큐브 조각화** 대화 상자의 **차원** 열에서 필터링 할 차원을 선택 합니다.  
  
4.  **계층 열의 목록을** 사용 하 여 계층의 수준을 선택 합니다.  
  
5.  **연산자** 열의 목록에서 필터 조건을 만드는 데 사용할 연산자를 선택 합니다.  
  
6.  **필터** 열에서 상자를 클릭 합니다.  
  
     지정한 계층 수준의 모든 멤버가 포함된 대화 상자가 열립니다.  
  
7.  필터를 적용할 멤버를 선택합니다.  
  
8.  멤버 대화 상자에서 **확인을** 클릭 합니다.  
  
9. **큐브 조각화** 대화 상자에서 **확인을** 클릭 합니다.  
  
     이렇게 하면 큐브 조각에서 정의한 대로 원본 큐브가 필터링됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [마이닝 구조 태스크 및 방법](data-mining/mining-structure-tasks-and-how-tos.md)   
 [새 OLAP 마이닝 구조 만들기](data-mining/create-a-new-olap-mining-structure.md)  
  
  
