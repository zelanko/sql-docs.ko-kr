---
title: '태스크 8: 정리 출력 분할 하는 변환 분할 조건부를 추가 합니다. | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d4ebe420-a4a9-4076-89d3-41abe726fc5c
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 6dc3b98e03a7940841bc97012c1a4e4220bb970d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172576"
---
# <a name="task-8-adding-conditional-split-transform-to-split-cleansing-output"></a>태스크 8: 조건부 분할 변환을 추가하여 정리 출력 분할
  이 변환에서는 데이터 흐름에 조건부 분할 변환을 추가합니다. 조건부 분할 변환은 데이터 내용에 따라 각 행을 서로 다른 출력으로 라우팅할 수 있습니다. 이 자습서에서 사용 하는 **레코드 상태** DQS 정리 변환에서 출력 열입니다. 이 자습서에서는 수정 레코드 또는 수정된 레코드만 MDS 서버에 업로드합니다. 따라서 경우 확인는 **레코드 상태** 은 **올바름** 또는 **Corrected**, 레코드를 MDS에 업로드 하기 전에 결합 합니다.  
  
1.  끌어서 놓기 **조건부 분할 변환** 에서 **일반적인** 섹션은 **SSIS 도구 상자** 에 **데이터 흐름** 아래의탭**Cleanse Supplier Data**합니다.  
  
2.  마우스 오른쪽 단추로 클릭 **조건부 분할**를 클릭 하 고 **이름 바꾸기**합니다. 형식 **Pick Correct and Corrected Records** 누릅니다 **ENTER**합니다.  
  
3.  연결 **Cleanse Supplier Data** 및 **Pick Correct and Corrected Records** 파란색 커넥터를 사용 하 여 합니다.  
  
     ![Cleanse Supplier 데이터에 올바른 및 수정 된 선택->](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-01.jpg "Cleanse Supplier 데이터에 올바른 및 수정 된 선택->")  
  
4.  두 번 클릭 **Pick Correct and Corrected Records** 에 **데이터 흐름** 탭 합니다.  
  
5.  변경 된 **기본 출력 이름** 화면 맨 아래에 **올바름**합니다.  
  
6.  확장 **열** 에 **왼쪽 상단 창**합니다.  
  
     ![조건부 분할 변환 편집기](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-02.jpg "조건부 분할 변환 편집기")  
  
7.  끌어서 놓기 **레코드 상태** 에 **조건** 열입니다.  
  
8.  형식 **= = "Corrected"** 옆에 **[Record Status]** 에 대 한는 **조건** 열입니다.  
  
9. 클릭 **사례 1** 에 **출력 이름 열**, 하도록 이름을 변경 하 고 **Corrected**합니다.  
  
10. 클릭 **확인** 를 닫으려면는 **조건부 분할 변환 편집기** 대화 상자.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 9: UNION ALL 변환을 추가하여 수정 및 수정된 레코드 결합](../../2014/tutorials/task-9-adding-union-all-transform-to-combine-correct-and-corrected-records.md)  
  
  