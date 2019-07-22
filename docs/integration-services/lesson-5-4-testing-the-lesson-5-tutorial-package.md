---
title: '4단계: 5단원 패키지 테스트 | Microsoft Docs'
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5215b77d-c2ec-4b25-a3de-ca49ea197d74
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 660c2ee9f09bcd3e8a4c883247bdded124561509
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67911469"
---
# <a name="lesson-5-4-test-the-lesson-5-package"></a>5-4단원: 5단원 패키지 테스트

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



런타임에 패키지는 패키지를 만들 때 지정한 원래 디렉터리 이름을 사용하지 않고 구성 변수에서 **Directory** 속성 값을 가져옵니다. 변수의 값은 **SSISTutorial.dtsConfig** XML 파일에서 가져옵니다.  
  
패키지가 런타임 동안 새 값으로 **Directory** 속성을 업데이트하도록 하려면 패키지를 실행하세요. 새 디렉터리에 세 개의 샘플 데이터 파일이 있으므로 데이터 흐름은 세 번만 실행됩니다.  
  
## <a name="checking-the-package-layout"></a>패키지 레이아웃 확인  
패키지를 테스트하려면 먼저 5단원 패키지의 제어 흐름과 데이터 흐름이 다음 다이어그램에 표시된 개체와 비슷한지 확인하세요.  
  
**제어 흐름**  
  
![패키지의 제어 흐름](../integration-services/media/task4lesson2control.gif "패키지의 제어 흐름")  
  
**데이터 흐름**  
  
![패키지의 데이터 흐름](../integration-services/media/task9lesson1data.gif "패키지의 데이터 흐름")  
  
## <a name="test-the-lesson-5-package"></a>5단원 패키지 테스트  
  
1.  **디버그** 메뉴에서 **디버깅 시작**을 선택합니다.  
  
2.  패키지의 실행이 완료된 후에 **디버그** 메뉴에서 **디버깅 중지**를 선택합니다.  
  
## <a name="next-lesson"></a>다음 단원  
[6단원: SSIS에서 프로젝트 배포 모델에 매개 변수 사용](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
  
  
  
