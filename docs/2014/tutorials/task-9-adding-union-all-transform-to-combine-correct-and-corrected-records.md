---
title: '작업 9: Union All 변환을 추가 하 여 올바른 레코드와 수정 된 레코드 결합 | Microsoft Docs'
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489641"
---
# <a name="task-9-adding-union-all-transform-to-combine-correct-and-corrected-records"></a>태스크 9: UNION ALL 변환을 추가하여 수정 및 수정된 레코드 결합
  이 작업에서는 UNION ALL 변환을 데이터 흐름에 추가합니다. UNION ALL 변환은 여러 개의 입력을 하나의 출력으로 결합합니다. 이 시나리오에서는 Correct 및 Corrected 레코드를 모두 하나의 스트림에 결합합니다.  
  
1.  **Union All** 변환을 **SSIS 도구 상자** 의 **일반** 섹션에서 **데이터 흐름** 탭으로 끌어서 놓고 **올바른 레코드 및 수정 된 레코드를 선택**합니다.  
  
2.  **데이터 흐름** 탭에서 **Union All** 변환을 마우스 오른쪽 단추로 클릭 하 고 **이름 바꾸기**를 클릭 합니다. **올바른 레코드와 수정 된 레코드 결합**을 입력 하 고 **enter**키를 누릅니다.  
  
     ![올바른 레코드 및 수정된 레코드 결합](../../2014/tutorials/media/et-addinguattocombinecacrecords-01.jpg "올바른 레코드 및 수정된 레코드 결합")  
  
3.  연결을 **선택 하 고** 수정 된 레코드를 수정 하 여 **데이터 흐름** 탭에서 파란색 커넥터를 사용 하 여 수정 된 레코드와 수정 된 **레코드를 결합** 합니다. **입력 출력 선택** 대화 상자가 표시 됩니다.  
  
4.  **입력 출력** 대화 상자에서 **출력** 에 대해 **수정** 을 선택 하 고 **확인**을 클릭 합니다.  
  
     ![입/출력 선택 대화 상자](../../2014/tutorials/media/et-addinguattocombinecacrecords-02.jpg "입/출력 선택 대화 상자")  
  
5.  커넥터 끝의 점을 왼쪽으로 끌어서 놓아 왼쪽으로 **올바른** 제목의 연결선을 이동 합니다.  
  
     ![올바른 레코드를 연결하여 올바른 데이터 및 수정된 레코드 결합](../../2014/tutorials/media/et-addinguattocombinecacrecords-03.jpg "올바른 레코드를 연결하여 올바른 데이터 및 수정된 레코드 결합")  
  
6.  **올바른 레코드 및 수정 된 레코드** 변환을 선택 하면 다른 파란색 커넥터가 표시 됩니다. 해당 파란색 커넥터를 끌어 **올바른 레코드와 수정 된 레코드를 결합**합니다.  
  
     ![수정된 레코드를 연결하여 올바른 데이터 및 수정된 레코드 결합](../../2014/tutorials/media/et-addinguattocombinecacrecords-04.jpg "수정된 레코드를 연결하여 올바른 데이터 및 수정된 레코드 결합")  
  
7.  이 **커넥터** 는 **수정**된 제목 이어야 합니다. 두 조건만 **정확** 하 고 **수정**되었으며 한 개의 조건이 이미 사용 되었으므로이 시간에는 **입력 출력 선택** 대화 상자가 표시 되지 않습니다. 커넥터가 겹치면 커넥터를 왼쪽 또는 오른쪽으로 끌어서 왼쪽과 오른쪽으로 각각 이동합니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 10: 유사 항목 그룹화 변환을 추가하여 중복 항목 식별](../../2014/tutorials/task-10-adding-fuzzy-group-transform-to-identify-duplicates.md)  
  
  
