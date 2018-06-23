---
title: (중급 데이터 마이닝 자습서) 시장 바구니 모델 수정 및 처리 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b6019413-aebd-4ff7-831a-644572ad88b1
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 96eb44713cd34fdcea81a7e5e4daf26739afdec1
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36311911"
---
# <a name="modifying-and-processing-the-market-basket-model-intermediate-data-mining-tutorial"></a>시장 바구니 모델 수정 및 처리(중급 데이터 마이닝 자습서)
  두 매개 변수의 기본값을 변경 해야 만든 연결 마이닝 모델을 처리 하기 전에: *지원* 및 *확률*합니다.  
  
-   *지원* 유효한 간주 되기 전에 규칙 존재 해야 하는 경우의 비율을 정의 합니다. 적어도 총 사례 수의 1% 이상에서 규칙을 발견하도록 지정합니다.  
  
-   *확률* 연결 해야 하는 가능성 정의 유효한 간주 되기 전에 이어야 합니다. 모든 연결의 확률은 적어도 10% 이상이라고 간주합니다.  
  
 지지도 및 확률을 늘리거나의 효과 대 한 자세한 내용은 참조 [Microsoft 연결 알고리즘 기술 참조](../../2014/analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md)합니다.  
  
 구조 및 매개 변수를 정의 하면는 **연결** 마이닝 모델의 모델을 처리 합니다.  
  
### <a name="to-adjust-the-parameters-of-the-association-model"></a>Association 모델의 매개 변수를 조정하려면  
  
1.  열기는 **마이닝 모델** 데이터 마이닝 디자이너의 탭 합니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **연결** 고 디자이너에서 표의 열에에서 **알고리즘 매개 변수를 열려는 알고리즘 매개 변수 설정** 대화 상자.  
  
3.  에 **값** 의 열은 **알고리즘 매개 변수** 대화 상자에서 다음 매개 변수 설정:  
  
     MINIMUM_PROBABILITY = 0.1  
  
     MINIMUM_SUPPORT = 0.01  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-process-the-mining-model"></a>마이닝 모델을 처리하려면  
  
1.  에 **마이닝 모델** 의 메뉴 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]선택, **마이닝 구조 및 모든 모델 처리 합니다.**  
  
2.  프로젝트를 빌드하여을 묻는 경고에서 클릭 **예**합니다.  
  
     **마이닝 구조 처리-Association** 대화 상자가 열립니다.  
  
3.  **실행**을 클릭합니다.  
  
     **처리 진행률** 대화 상자가 열리고 모델 처리에 대 한 정보를 표시 합니다. 새 구조 및 모델을 처리하는 데에는 시간이 걸릴 수 있습니다.  
  
4.  처리가 완료 되 면 클릭 **닫기** 종료 하 고 **처리 진행률** 대화 상자.  
  
5.  클릭 **닫기** 를 닫습니다는 **마이닝 구조 처리-Association** 대화 상자.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [시장 바구니 모델 탐색 시 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/exploring-the-market-basket-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [처리 요구 사항 및 고려 사항 &#40;데이터 마이닝&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  