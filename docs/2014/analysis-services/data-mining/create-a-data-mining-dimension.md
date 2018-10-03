---
title: 데이터 마이닝 차원 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], dimensions
ms.assetid: 9f0c39e5-3516-43ab-b203-f3f6dbcff89a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: feff90d769016492f10c3699ebd563aac13a84b7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48117316"
---
# <a name="create-a-data-mining-dimension"></a>데이터 마이닝 차원 만들기
  마이닝 구조가 OLAP 큐브를 기반으로 하는 경우에는 마이닝 모델의 내용을 포함하는 차원을 만들 수 있습니다. 그런 다음 차원을 다시 원본 큐브에 통합할 수 있습니다.  
  
 또한 차원을 찾아보거나 차원을 사용하여 모델 결과를 탐색하거나 MDX를 사용하여 차원을 쿼리할 수 있습니다.  
  
### <a name="to-create-a-data-mining-dimension"></a>데이터 마이닝 차원을 만들려면  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]의 데이터 마이닝 디자이너에서 **마이닝 구조** 탭이나 **마이닝 모델** 탭을 선택합니다.  
  
2.  **마이닝 모델** 메뉴에서 **데이터 마이닝 차원 만들기**를 선택합니다.  
  
     **데이터 마이닝 차원 만들기** 대화 상자가 열립니다.  
  
3.  **데이터 마이닝 차원 만들기** 대화 상자의 **모델 이름** 목록에서 OLAP 마이닝 모델을 선택합니다.  
  
4.  **차원 이름** 입력란에 새 데이터 마이닝 차원의 이름을 입력합니다.  
  
5.  새 데이터 마이닝 차원을 포함하는 큐브를 만들려면 **큐브 만들기**를 선택합니다. **큐브 만들기**를 선택한 후에는 큐브의 새 이름을 입력할 수 있습니다.  
  
6.  **확인**을 클릭합니다.  
  
     데이터 마이닝 차원이 생성되어 솔루션 탐색기의 **차원** 폴더에 추가됩니다. **큐브 만들기**를 선택한 경우에는 새 큐브도 생성되어 **큐브** 폴더에 추가됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [마이닝 구조 태스크 및 방법](mining-structure-tasks-and-how-tos.md)  
  
  
