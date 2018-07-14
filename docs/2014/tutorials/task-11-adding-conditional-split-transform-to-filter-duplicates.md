---
title: '태스크 11: 중복 항목을 필터링 하는 변환 분할 조건부를 추가 합니다. | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3094bd57-5cf4-4860-bf51-fadd1b309f94
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ae4b77e5788ac21e6962ad7f4a6679982363cd67
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185660"
---
# <a name="task-11-adding-conditional-split-transform-to-filter-duplicates"></a>태스크 11: 조건부 분할 변환을 추가하여 중복 항목 필터링
  이 작업에서는 조건부 분할 변환을 데이터 흐름에 추가합니다. 이 변환은 들어오는 레코드 집합에서 중복 항목을 필터링하는 데 도움이 됩니다. 유사 항목 그룹 변환은 일치하는 것으로 발견된 레코드를 그룹화하고 레코드 중 하나를 피벗 레코드로 선택합니다. 그룹의 모든 레코드는 동일한 _key_out 값을 갖습니다. 그룹의 피벗 레코드는 _key_in 값이 _key_out 값과 동일합니다. 그룹의 다른 레코드는 _key_in 및 _key_out 값이 서로 다릅니다. 따라서 _key_in==_key_out 조건을 사용해서 필터링하면 그룹의 피벗 행만 표시됩니다.  
  
1.  끌어서 놓기 **조건부 분할** 에서 변환 **일반적인** 섹션의 **SSIS 도구 상자** 에 **데이터 흐름** 탭 합니다.  
  
2.  마우스 오른쪽 단추로 클릭 **조건부 분할 변환을** 에 **데이터 흐름** 탭을 클릭 **이름 바꾸기**합니다. 형식 **Filter Duplicates** 누릅니다 **ENTER**합니다.  
  
3.  연결 **일치 하는 Id 공급자 그룹화** 하 **중복 항목을 필터링**합니다.  
  
4.  두 번 클릭 **Filter Duplicates** 시작 하는 **조건부 분할 변환 편집기** 대화 상자.  
  
5.  확장 **열** 왼쪽 위 창에서.  
  
6.  끌어서 놓기 **_key_in** 에 **조건** 열입니다.  
  
7.  형식 옆에 (같음) = = **_key_in** 으로 끌어서 놓습니다 **_key_out**합니다.  
  
8.  클릭 **사례 1** 에 **출력 이름** 열을 입력 **Unique Records**, 키를 누릅니다 **ENTER**합니다.  
  
     ![조건부 분할 변환 편집기](../../2014/tutorials/media/et-addingconditionalsplittransformtofilterduplicates.jpg "조건부 분할 변환 편집기")  
  
9. 클릭 **확인** 닫으려면 합니다 **조건부 분할 변환 편집기** 대화 상자.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 12: 파생 열 변환을 추가하여 MDS에 필요한 열 추가](../../2014/tutorials/task-12-adding-derived-column-transform-to-add-columns-required-by-mds.md)  
  
  
