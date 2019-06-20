---
title: '3단계: 6 단원 패키지 테스트 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: c184c92d-948f-4037-a502-5fabd909c84c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c69c75c9dff4bf8d0542dae71cddcf1a431ab063
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62890859"
---
# <a name="step-3-testing-the-lesson-6-package"></a>3단계: 6단원 패키지 테스트
  런타임에서 패키지는 VarFolderName 매개 변수로부터 Directory 속성 값을 가져옵니다.  
  
 패키지가 런타임에 새 값으로 Directory 속성을 업데이트하도록 하려면 패키지를 실행해 보십시오. 예제 데이터 파일이 3개만 새 디렉터리에 복사되었으므로 데이터 흐름이 원래 폴더에 있는 파일 14개를 반복하지 않고 세 번만 실행됩니다.  
  
## <a name="checking-the-package-layout"></a>패키지 레이아웃 확인  
 패키지를 테스트하려면 먼저 6단원 패키지의 제어 흐름과 데이터 흐름에 다음 다이어그램에 표시된 개체가 있는지 확인해야 합니다. 제어 흐름은 5단원의 제어 흐름과 동일해야 합니다. 데이터 흐름은 5단원의 데이터 흐름과 동일해야 합니다.  
  
 **제어 흐름**  
  
 ![제어 흐름](../../2014/tutorials/media/task3lesson6control.jpg "제어 흐름")  
  
 **데이터 흐름**  
  
 ![데이터 흐름](../../2014/tutorials/media/task3lesson6data.jpg "데이터 흐름")  
  
### <a name="to-test-the-lesson-6-tutorial-package"></a>6 단원 자습서 패키지를 테스트하려면  
  
1.  디버그 메뉴에서 디버깅 시작을 클릭합니다.  
  
2.  패키지의 실행이 완료된 후에 디버그 메뉴에서 디버깅 중지를 클릭합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [4단계: 6 단원 패키지 배포](../integration-services/lesson-6-4-deploying-the-lesson-6-package.md)  
  
  
