---
title: '작업 8: 분할 정리 출력에 조건부 분할 변환 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: d4ebe420-a4a9-4076-89d3-41abe726fc5c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d5a55f0694094e6fe88a42946bcff34f420210f4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489678"
---
# <a name="task-8-adding-conditional-split-transform-to-split-cleansing-output"></a>태스크 8: 조건부 분할 변환을 추가하여 정리 출력 분할
  이 변환에서는 데이터 흐름에 조건부 분할 변환을 추가합니다. 조건부 분할 변환은 데이터 내용에 따라 각 행을 서로 다른 출력으로 라우팅할 수 있습니다. 이 자습서에서는 DQS 정리 변환의 **레코드 상태** 출력 열을 사용 합니다. 이 자습서에서는 수정 레코드 또는 수정된 레코드만 MDS 서버에 업로드합니다. 따라서 레코드 **상태가** **올바른지** 또는 **수정**되었는지 확인 하 고 레코드를 MDS에 업로드 하기 전에 결합 합니다.  
  
1.  **SSIS 도구 상자** 의 **일반** 섹션에서 **공급자 데이터 정리**의 **데이터 흐름** 탭으로 **조건부 분할 변환** 을 끌어서 놓습니다.  
  
2.  **조건부 분할**을 마우스 오른쪽 단추로 클릭 하 고 **이름 바꾸기**를 클릭 합니다. **선택 수정 및 수정 된 레코드** 를 입력 하 고 **enter**키를 누릅니다.  
  
3.  **정리 공급자 데이터** 를 연결 하 고 파란색 커넥터를 사용 하 여 **수정 및** 수정 된 레코드를 선택 합니다.  
  
     ![공급자 데이터 정리-> 수정 & 수정 됨](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-01.jpg "공급자 데이터 정리 -> 올바른 데이터 및 수정된 데이터 선택")  
  
4.  **데이터 흐름** 탭에서 **수정 및 수정 된 레코드 선택** 을 두 번 클릭 합니다.  
  
5.  화면 맨 아래에 있는 **기본 출력 이름을** **수정**합니다.  
  
6.  **왼쪽 위 창**에서 **열** 을 확장 합니다.  
  
     ![조건부 분할 변환 편집기](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-02.jpg "조건부 분할 변환 편집기")  
  
7.  **레코드 상태** 를 **조건** 열로 끌어서 놓습니다.  
  
8.  **조건** 열의 **[레코드 상태]** 옆에 **= = "수정 됨"** 을 입력 합니다.  
  
9. **출력 이름 열**에서 **Case 1** 을 클릭 하 고 이름을 **수정**됨으로 변경 합니다.  
  
10. **확인** 을 클릭 하 여 **조건부 분할 변환 편집기** 대화 상자를 닫습니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 9: UNION ALL 변환을 추가하여 수정 및 수정된 레코드 결합](../../2014/tutorials/task-9-adding-union-all-transform-to-combine-correct-and-corrected-records.md)  
  
  
