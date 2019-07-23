---
title: '9단계: 1단원 자습서 패키지 테스트 | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 9aee7acf-797b-46f2-830d-80ab64a9f0b6
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 437e919b8dfba5d375a80fc53267a539d907aaa4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902508"
---
# <a name="lesson-1-9-test-the-lesson-1-package"></a>1-9단원: 1단원 패키지 테스트

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



이 자습서에서는 다음 작업을 수행했습니다.  
  
-   새 [!INCLUDE[ssIS](../includes/ssis-md.md)] 프로젝트를 만들었습니다.  
  
-   패키지가 원본 및 대상 데이터에 연결하도록 연결 관리자를 구성했습니다.  
  
-   플랫 파일 원본에서 데이터를 가져오고 데이터에 필요한 조회 변환을 수행하고 대상의 데이터를 구성하는 데이터 흐름을 추가했습니다.  
  
이제 패키지가 완료되어 테스트할 준비가 되었습니다.
  
## <a name="check-the-package-components"></a>패키지 구성 요소 확인
  
패키지를 테스트하려면 먼저 1단원 패키지의 제어 흐름과 데이터 흐름에 다음 다이어그램에 표시된 개체가 있는지 확인합니다.  
  
**제어 흐름** 
  
![패키지의 제어 흐름](../integration-services/media/task9lesson1control.gif "패키지의 제어 흐름")  
  
**데이터 흐름**  
  
![패키지의 데이터 흐름](../integration-services/media/task9lesson1data.gif "패키지의 데이터 흐름")  
  
## <a name="run-the-lesson-1-package"></a>1단원 패키지 실행  
  
1.  **디버그** 메뉴에서 **디버깅 시작**을 선택합니다.  
  
    패키지가 실행되어 1097개의 행이 **AdventureWorksDW2012**의 **NewFactCurrencyRate** 팩트 테이블에 성공적으로 추가됩니다. 이 결과를 확인하려면 **데이터 흐름** 탭을 선택합니다.
  
2.  패키지의 실행이 완료된 후에 **디버그** 메뉴에서 **디버깅 중지**를 선택합니다.  
  
## <a name="go-to-next-lesson"></a>다음 단원으로 이동
[2단원: SSIS를 사용하여 루핑 추가](../integration-services/lesson-2-adding-looping-with-ssis.md)  
  
## <a name="see-also"></a>관련 항목:  
[프로젝트 및 패키지 실행](packages/run-integration-services-ssis-packages.md) 
  
  
  
