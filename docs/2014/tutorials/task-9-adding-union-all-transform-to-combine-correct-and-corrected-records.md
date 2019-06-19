---
title: '태스크 9: Union All을 추가 하 여 수정 및 수정 된 레코드 결합 변환 | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 24ba466d-a7d3-49e7-9111-b348399c9e58
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 93b160b6e513ad866126df8b401b82ee1270be84
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489641"
---
# <a name="task-9-adding-union-all-transform-to-combine-correct-and-corrected-records"></a>태스크 9: Union All 변환을 추가하여 수정 및 수정된 레코드 결합
  이 작업에서는 UNION ALL 변환을 데이터 흐름에 추가합니다. UNION ALL 변환은 여러 개의 입력을 하나의 출력으로 결합합니다. 이 시나리오에서는 Correct 및 Corrected 레코드를 모두 하나의 스트림에 결합합니다.  
  
1.  끌어서 놓기 **Union All** 에서 변환 **일반적인** 섹션의 **SSIS 도구 상자** 에 **데이터 흐름** 아래에배치하고탭**수정 및 수정 된 레코드 선택**합니다.  
  
2.  마우스 오른쪽 단추로 클릭 **Union All** 에서 변환 된 **데이터 흐름** 탭을 클릭 **이름 바꾸기**합니다. 형식 **Combine Correct and Corrected Records**, 누릅니다 **ENTER**합니다.  
  
     ![수정 및 수정 된 Reocrds 결합](../../2014/tutorials/media/et-addinguattocombinecacrecords-01.jpg "수정 및 수정 된 Reocrds 결합")  
  
3.  연결 **Pick Correct and Corrected Records** 하 **Combine Correct and Corrected Records** 에 **데이터 흐름** 파란색 커넥터를 사용 하 여 탭 합니다. 표시 되어야 합니다 **입/출력 선택** 대화 상자.  
  
4.  에 **입력 출력** 대화 상자에서 **올바름** 에 대 한 **출력** 클릭 **확인**합니다.  
  
     ![출력 선택 대화 상자를 입력](../../2014/tutorials/media/et-addinguattocombinecacrecords-02.jpg "출력 선택 대화 상자를 입력 합니다.")  
  
5.  이라는 커넥터를 이동할 **수정** 왼쪽으로 끌어서 왼쪽으로 커넥터의 끝에서 점을 삭제 합니다.  
  
     ![연결 수정 및 수정 된 결합 잘못](../../2014/tutorials/media/et-addinguattocombinecacrecords-03.jpg "수정 및 수정 된 결합 하려면 올바른 연결")  
  
6.  선택 하는 경우 **Pick Correct and Corrected Records** 변환 다른 파란색 커넥터가 표시 됩니다. 파란색 커넥터를 끌어 **Combine Correct and Corrected Records**합니다.  
  
     ![Combine Correct and 수정 하려면 수정 된 연결](../../2014/tutorials/media/et-addinguattocombinecacrecords-04.jpg "Combine Correct and 수정 하려면 수정 된 연결")  
  
7.  이렇게 **connector** 이름이 **수정**합니다. 두 조건을 했으므로 **올바름** 및 **수정 됨**, 하나의 조건이 이미 사용 되었으며 및, **입/출력 선택** 대화 상자가이 현재 표시 되지 않습니다. 커넥터가 겹치면 커넥터를 왼쪽 또는 오른쪽으로 끌어서 왼쪽과 오른쪽으로 각각 이동합니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 10: 유사 항목 그룹화 변환을 추가 하 여 중복 항목 식별](../../2014/tutorials/task-10-adding-fuzzy-group-transform-to-identify-duplicates.md)  
  
  
