---
title: 시장 바구니 모델 수정 및 처리 (중급 데이터 마이닝 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b6019413-aebd-4ff7-831a-644572ad88b1
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4987e3497b7d52ff11f8f52bc403105340f7f508
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63301367"
---
# <a name="modifying-and-processing-the-market-basket-model-intermediate-data-mining-tutorial"></a>시장 바구니 모델 수정 및 처리(중급 데이터 마이닝 자습서)
  만든 연결 마이닝 모델을 처리 하기 전에 두 매개 변수 ( *지원* 및 *확률*)의 기본값을 변경 해야 합니다.  
  
-   *지원은* 규칙이 유효한 것으로 간주 되기 전에 존재 해야 하는 사례의 비율을 정의 합니다. 적어도 총 사례 수의 1% 이상에서 규칙을 발견하도록 지정합니다.  
  
-   *확률* 은 연결이 유효한 것으로 간주 되기 전에 연결 해야 하는 가능성을 정의 합니다. 모든 연결의 확률은 적어도 10% 이상이라고 간주합니다.  
  
 지원 및 확률을 늘리거나 줄이는 효과에 대 한 자세한 내용은 [Microsoft 연결 알고리즘 기술 참조](../../2014/analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md)를 참조 하세요.  
  
 **연결** 마이닝 모델에 대 한 구조와 매개 변수를 정의한 후에는 모델을 처리 합니다.  
  
### <a name="to-adjust-the-parameters-of-the-association-model"></a>Association 모델의 매개 변수를 조정하려면  
  
1.  데이터 마이닝 디자이너의 **마이닝 모델** 탭을 엽니다.  
  
2.  디자이너의 표에서 **연결** 열을 마우스 오른쪽 단추로 클릭 하 고 **알고리즘 매개 변수 설정을 선택 하 여 알고리즘 매개 변수 대화 상자를 엽니다** .  
  
3.  **알고리즘 매개 변수** 대화 상자의 **값** 열에서 다음 매개 변수를 설정 합니다.  
  
     MINIMUM_PROBABILITY = 0.1  
  
     MINIMUM_SUPPORT = 0.01  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-process-the-mining-model"></a>마이닝 모델을 처리하려면  
  
1.  의 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] **마이닝 모델** 메뉴에서 **마이닝 구조 및 모든 모델 처리** 를 선택 합니다.  
  
2.  프로젝트를 빌드 및 배포할지를 요청 하는 경고에서 **예**를 클릭 합니다.  
  
     **마이닝 구조 처리-연결** 대화 상자가 열립니다.  
  
3.  **실행**을 클릭합니다.  
  
     **처리 진행률** 대화 상자가 열리고 모델 처리에 대 한 정보를 표시 합니다. 새 구조 및 모델을 처리하는 데에는 시간이 걸릴 수 있습니다.  
  
4.  처리가 완료 되 면 **닫기** 를 클릭 하 여 처리 **진행률** 대화 상자를 종료 합니다.  
  
5.  **닫기** 를 다시 클릭 하 여 **마이닝 구조 처리-연결** 대화 상자를 종료 합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [시장 바구니 모델 탐색 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/exploring-the-market-basket-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝&#41;&#40;처리 요구 사항 및 고려 사항](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
