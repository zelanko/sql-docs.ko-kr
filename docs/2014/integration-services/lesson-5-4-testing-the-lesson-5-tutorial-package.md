---
title: '4단계: 5 단원 자습서 패키지 테스트 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5215b77d-c2ec-4b25-a3de-ca49ea197d74
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 29154120646f74da7471f44a1630b3d99afefa4f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52747485"
---
# <a name="step-4-testing-the-lesson-5-tutorial-package"></a>4단계: 5단원 자습서 패키지 테스트
  런타임에 패키지는 패키지를 만들 때 지정한 원래 디렉터리 이름을 사용하지 않고 런타임에 업데이트된 변수에서 `Directory` 속성 값을 가져옵니다. SSISTutorial.dtsConfig 파일을 사용하여 변수의 값이 채워집니다.  
  
 패키지가 런타임에 새 값으로 Directory 속성을 업데이트하도록 하려면 패키지를 실행해 보십시오. 예제 데이터 파일이 3개만 새 디렉터리에 복사되었으므로 데이터 흐름이 원래 폴더에 있는 파일 14개를 반복하지 않고 세 번만 실행됩니다.  
  
## <a name="checking-the-package-layout"></a>패키지 레이아웃 확인  
 패키지를 테스트하려면 먼저 5단원 패키지의 제어 흐름과 데이터 흐름에 다음 다이어그램에 표시된 개체가 있는지 확인해야 합니다. 제어 흐름은 4단원의 제어 흐름과 동일해야 합니다. 데이터 흐름은 4단원의 데이터 흐름과 동일해야 합니다.  
  
 **제어 흐름**  
  
 ![패키지의 제어 흐름](../../2014/tutorials/media/task4lesson2control.gif "패키지의 제어 흐름")  
  
 **데이터 흐름**  
  
 ![패키지의 데이터 흐름](../../2014/tutorials/media/task9lesson1data.gif "패키지의 데이터 흐름")  
  
### <a name="to-test-the-lesson-5-tutorial-package"></a>5단원 자습서 패키지를 테스트하려면  
  
1.  **디버그** 메뉴에서 **디버깅 시작**을 클릭합니다.  
  
2.  패키지의 실행이 완료된 후에 **디버그** 메뉴에서 **디버깅 중지**를 클릭합니다.  
  
## <a name="next-lesson"></a>다음 단원  
 [6 단원: 매개 변수를 사용 하 여 프로젝트 배포 모델을 사용 하 여](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
  
  
