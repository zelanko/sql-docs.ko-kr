---
title: '4단계: 2단원 자습서 패키지 테스트 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0e8c0a25-8f79-41df-8ed2-f82a74b129cd
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1a9b8361c83201fa2e3c6aa0c6a091e09f7c12f3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62767491"
---
# <a name="step-4-testing-the-lesson-2-tutorial-package"></a>4단계: 2단원 자습서 패키지 테스트
  Foreach 루프 컨테이너와 플랫 파일 연결 관리자가 이제 구성되었으므로 2단원 패키지에서는 Sample Data 폴더에 있는 14개의 플랫 파일을 반복 처리할 수 있습니다. 지정한 파일 이름 기준과 일치하는 파일 이름을 찾을 때마다 Foreach 루프 컨테이너는 사용자 정의 변수를 해당 파일 이름으로 채웁니다. 이에 따라 이 변수가 플랫 파일 연결 관리자의 ConnectionString 속성을 업데이트하면 새 플랫 파일에 연결됩니다. Foreach 루프 컨테이너는 폴더에 있는 다음 파일에 연결하기 전에 새 플랫 파일의 데이터에 대해 수정되지 않은 데이터 흐름 태스크를 실행합니다.  
  
 다음 절차를 사용하여 패키지에 추가한 새 루핑 기능을 테스트할 수 있습니다.  
  
> [!NOTE]  
>  1단원에서 패키지를 실행한 경우 이 단원에서 패키지를 실행하기 전에 AdventureWorksDW2012에서 dbo.FactCurrency의 레코드를 삭제해야 하며, 그렇지 않으면 패키지가 실패하고 기본 키 제약 조건 위반을 나타내는 오류가 나타납니다. 디버그/디버깅 시작(F5)을 선택하여 패키지를 실행하면 1단원 및 2단원이 모두 실행되므로 같은 오류가 발생합니다. 2단원에서는 1단원에서 이미 삽입한 레코드를 삽입하려고 시도합니다.  
  
## <a name="checking-the-package-layout"></a>패키지 레이아웃 확인  
 패키지를 테스트하려면 먼저 2단원 패키지의 제어 흐름과 데이터 흐름에 다음 다이어그램에 표시된 개체가 있는지 확인해야 합니다. 데이터 흐름은 1단원의 데이터 흐름과 동일해야 합니다.  
  
 **제어 흐름**  
  
 ![패키지의 제어 흐름](../../2014/tutorials/media/task4lesson2control.gif "패키지의 제어 흐름")  
  
 **데이터 흐름**  
  
 ![패키지의 데이터 흐름](../../2014/tutorials/media/task9lesson1data.gif "패키지의 데이터 흐름")  
  
### <a name="to-test-the-lesson-2-tutorial-package"></a>2단원 자습서 패키지를 테스트하려면  
  
1.  **솔루션 탐색기**에서 **Lesson 2.dtsx** 를 마우스 오른쪽 단추로 클릭한 다음 **패키지 실행**을 클릭합니다.  
  
     패키지가 실행됩니다. 출력 창에서 각 루프의 상태를 확인 하거나 **진행률** 탭을 클릭 하 여 확인할 수 있습니다. 예를 들어 Currency_VEB 파일에서 대상 테이블에 1097 줄이 추가 된 것을 볼 수 있습니다.  
  
2.  패키지의 실행이 완료된 후에 **디버그** 메뉴에서 **디버깅 중지**를 클릭합니다.  
  
## <a name="next-lesson"></a>다음 단원  
 [5단원: 패키지 배포 모델을 위한 패키지 구성 추가](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
  
## <a name="see-also"></a>참고 항목  
 [프로젝트 및 패키지 실행](packages/run-integration-services-ssis-packages.md)  
  
  
