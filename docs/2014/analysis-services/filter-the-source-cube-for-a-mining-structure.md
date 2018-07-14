---
title: 마이닝 구조에 대 한 원본 큐브 필터링 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- slice cubes [Analysis Services]
- mining structures [Analysis Services], filtering source cube
- cubes [Analysis Services], slicing
- filtering data [Analysis Services]
ms.assetid: 05dce7e1-2fe5-4500-bacf-c1a8a76e1424
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 10ad6c295f61de1f50688bb8f52b12268756860a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37226653"
---
# <a name="filter-the-source-cube-for-a-mining-structure"></a>마이닝 구조에 대한 원본 큐브 필터링
  다차원 모델 (OLAP 큐브)에서 데이터를 기반으로 하는 마이닝 구조를 만들 수 있습니다 *조각* 마이닝 구조의 기반이 되는 큐브. 조각화하면 마이닝 모델 학습에 사용되는 데이터에 대한 일종의 필터로 데이터 하위 집합을 만들 수 있습니다.  
  
### <a name="to-slice-a-cube"></a>큐브를 조각화하려면  
  
1.  데이터 마이닝 디자이너에서 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]를 선택 합니다 **Mining Structure** 탭 또는 **마이닝 모델** 탭 합니다.  
  
2.  에 **마이닝 모델** 메뉴에서 **마이닝 구조 큐브 조각화 정의**합니다.  
  
     합니다 **큐브 조각화** 대화 상자가 열립니다.  
  
3.  에 **차원** 열의 합니다 **큐브 조각화** 대화 상자에서 필터링 할 차원을 선택 합니다.  
  
4.  목록을 사용 하 여 계층의 수준을 선택 합니다 **계층** 열입니다.  
  
5.  목록에서 연산자를 선택 합니다 **연산자** 필터 조건을 만드는 데 사용할 열입니다.  
  
6.  상자를 클릭 합니다 **필터** 열입니다.  
  
     지정한 계층 수준의 모든 멤버가 포함된 대화 상자가 열립니다.  
  
7.  필터를 적용할 멤버를 선택합니다.  
  
8.  클릭 **확인** 멤버 대화 상자에서.  
  
9. 클릭 **확인** 에 **큐브 조각화** 대화 상자.  
  
     이렇게 하면 큐브 조각에서 정의한 대로 원본 큐브가 필터링됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [마이닝 구조 태스크 및 방법](data-mining/mining-structure-tasks-and-how-tos.md)   
 [새 OLAP 마이닝 구조 만들기](data-mining/create-a-new-olap-mining-structure.md)  
  
  
