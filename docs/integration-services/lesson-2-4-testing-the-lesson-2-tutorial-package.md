---
title: '4단계: 2단원 자습서 패키지 테스트 | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 0e8c0a25-8f79-41df-8ed2-f82a74b129cd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1b17fc99cc7746739f381ba22f55a973d55497a1
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71283560"
---
# <a name="lesson-2-4-test-the-lesson-2-tutorial-package"></a>2-4단원: 2단원 자습서 패키지 테스트

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Foreach 루프 컨테이너와 플랫 파일 연결 관리자가 이제 구성되었으므로 2단원 패키지에서는 Sample Data 폴더에 있는 14개의 플랫 파일을 반복할 수 있습니다. 파일 이름이 지정된 기준과 일치할 때마다 Foreach 루프 컨테이너는 사용자 정의 변수를 해당 파일 이름으로 채웁니다. 이에 따라 이 변수는 해당 플랫 파일에 연결하는 플랫 파일 연결 관리자의 ConnectionString 속성을 업데이트합니다. 그런 다음, Foreach 루프 컨테이너는 해당 플랫 파일의 데이터에 대해 수정되지 않은 데이터 흐름 태스크를 실행합니다.  
  
> [!NOTE]  
> 1단원에서 패키지를 실행하는 경우 이 단원에서 패키지를 실행하기 전에 AdventureWorksDW2012 데이터베이스의 dbo.NewFactCurrencyRate 테이블에서 레코드를 삭제해야 합니다. 2단원에서 1단원에 이미 삽입된 레코드를 삽입하려고 시도하면 오류가 발생합니다.  
  
## <a name="check-the-package-layout"></a>패키지 레이아웃 확인  
패키지를 테스트하려면 먼저 2단원 패키지의 제어 흐름과 데이터 흐름에 다음 다이어그램에 표시된 개체가 있는지 확인합니다. 2단원의 데이터 흐름은 1단원과 같습니다.  
  
**제어 흐름**  
  
![패키지의 제어 흐름](../integration-services/media/task4lesson2control.gif "패키지의 제어 흐름")  
  
**데이터 흐름**  
  
![패키지의 데이터 흐름](../integration-services/media/task9lesson1data.gif "패키지의 데이터 흐름")  
  
## <a name="test-the-lesson-2-tutorial-package"></a>2단원 자습서 패키지 테스트  
  
1.  **솔루션 탐색기**에서 **Lesson 2.dtsx**를 마우스 오른쪽 단추로 클릭하고 **패키지 실행**을 선택합니다.  
  
    패키지를 실행합니다. **출력** 창에서 또는 **진행률** 탭을 선택하여 각 루프의 상태를 확인할 수 있습니다. 예를 들어 Currency_VEB.txt 파일에서 대상 테이블로 1097개의 행이 추가되었음을 확인할 수 있습니다.  
  
2.  패키지의 실행이 완료된 후에 **디버그** 메뉴에서 **디버깅 중지**를 선택합니다.  
  
## <a name="go-to-next-lesson"></a>다음 단원으로 이동  
[3단원: SSIS를 사용하여 로깅 추가](../integration-services/lesson-3-add-logging-with-ssis.md)  
  
## <a name="see-also"></a>참고 항목  
[프로젝트 및 패키지 실행](../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
  
  

