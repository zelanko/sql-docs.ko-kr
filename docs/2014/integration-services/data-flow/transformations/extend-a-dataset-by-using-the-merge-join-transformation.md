---
title: 병합 조인 변환을 사용하여 데이터 집합 확장 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Merge Join transformation
- datasets [Integration Services], joining
- datasets [Integration Services], extending
- joining datasets [Integration Services]
ms.assetid: 9e512c3c-f89b-45f3-8281-cdb8f35a2b1f
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 27d88e5105ddbbdbc8e9f8b5826b658921db2a1f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089603"
---
# <a name="extend-a-dataset-by-using-the-merge-join-transformation"></a>병합 조인 변환을 사용하여 데이터 집합 확장
  병합 조인 변환을 추가 및 구성하려면 패키지에 적어도 하나 이상의 데이터 흐름 태스크와 병합 조인 변환에 입력을 제공하는 두 개의 데이터 흐름 구성 요소가 이미 들어 있어야 합니다.  
  
 병합 조인 변환에는 두 개의 정렬된 입력이 필요합니다. 자세한 내용은 [병합 및 병합 조인 변환을 위한 데이터 정렬](sort-data-for-the-merge-and-merge-join-transformations.md)을 참조하세요.  
  
### <a name="to-extend-a-dataset"></a>데이터 집합을 확장하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **데이터 흐름** 탭을 클릭한 다음 **도구 상자**에서 병합 조인 변환을 디자인 화면으로 끌어 옵니다.  
  
4.  데이터 원본이나 이전 변환에서 연결선을 병합 조인 변환으로 끌어서 병합 조인 변환을 데이터 흐름에 연결합니다.  
  
5.  병합 조인 변환을 두 번 클릭합니다.  
  
6.  **병합 조인 변환 편집기** 대화 상자의 **조인 유형** 목록에서 사용할 조인 유형을 선택합니다.  
  
    > [!NOTE]  
    >  **왼쪽 우선 외부 조인** 유형을 선택한 경우 **입력 바꾸기** 를 클릭하여 입력을 전환하고 왼쪽 우선 외부 조인을 오른쪽 우선 외부 조인으로 변환할 수 있습니다.  
  
7.  왼쪽 입력의 열을 오른쪽 입력의 열로 끌어서 조인 열을 지정합니다. 열 이름이 같은 경우 **조인 키** 확인란을 선택하면 병합 조인 변환이 조인을 자동으로 만듭니다.  
  
    > [!NOTE]  
    >  정렬 위치가 동일한 열 사이에서만 조인을 만들 수 있으며, 정렬 위치에 지정된 순서에 따라 조인을 만들어야 합니다. 순서를 다르게 해서 조인을 만들면 **병합 조인 변환 편집기** 에 생략된 정렬 순서 위치에 대한 추가 조인을 만들라는 메시지가 표시됩니다.  
  
    > [!NOTE]  
    >  기본적으로 출력이 조인 열에서 정렬됩니다.  
  
8.  왼쪽 및 오른쪽 입력에서 출력에 포함시킬 추가 열의 확인란을 선택합니다. 조인 열은 기본적으로 포함됩니다.  
  
9. 필요에 따라 **출력 별칭** 열에서 출력 열의 이름을 업데이트합니다.  
  
10. **확인**을 클릭합니다.  
  
11. 업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [병합 조인 변환](merge-join-transformation.md)   
 [Integration Services 변환](integration-services-transformations.md)   
 [Integration Services 경로](../integration-services-paths.md)   
 [데이터 흐름 태스크] ((.. /.. /control-flow/data-flow-task.md)  
  
  