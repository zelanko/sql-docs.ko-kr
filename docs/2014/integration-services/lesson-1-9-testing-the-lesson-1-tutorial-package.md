---
title: '9단계: 1단원 자습서 패키지 테스트 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 9aee7acf-797b-46f2-830d-80ab64a9f0b6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ba98c694b99eb1ab81836a5d1f23a5cd4ea0d545
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48197003"
---
# <a name="step-9-testing-the-lesson-1-tutorial-package"></a>9단계: 1단원 자습서 패키지 테스트
  이 단원에서는 다음 태스크를 수행했습니다.  
  
-   새 [!INCLUDE[ssIS](../includes/ssis-md.md)] 프로젝트를 만들었습니다.  
  
-   패키지에서 원본 및 대상 데이터에 연결하는 데 필요한 연결 관리자를 구성했습니다.  
  
-   플랫 파일 원본에서 데이터를 가져오고 데이터에 필요한 조회 변환을 수행하고 대상의 데이터를 구성하는 데이터 흐름을 추가했습니다.  
  
 이제 패키지가 완료되었습니다! 패키지를 테스트하십시오.  
  
## <a name="checking-the-package-layout"></a>패키지 레이아웃 확인  
 패키지를 테스트하려면 먼저 1단원 패키지의 제어 흐름과 데이터 흐름에 다음 다이어그램에 표시된 개체가 있는지 확인해야 합니다.  
  
 **제어 흐름**  
  
 ![패키지의 제어 흐름](../../2014/tutorials/media/task9lesson1control.gif "패키지의 제어 흐름")  
  
 **데이터 흐름**  
  
 ![패키지의 데이터 흐름](../../2014/tutorials/media/task9lesson1data.gif "패키지의 데이터 흐름")  
  
### <a name="to-run-the-lesson-1-tutorial-package"></a>1단원 자습서 패키지를 실행하려면  
  
1.  **디버그** 메뉴에서 **디버깅 시작**을 클릭합니다.  
  
     패키지가 실행되어 1097개의 행이 **AdventureWorksDW2012** 의 **FactCurrency**팩트 테이블에 성공적으로 추가됩니다.  
  
2.  패키지의 실행이 완료된 후에 **디버그** 메뉴에서 **디버깅 중지**를 클릭합니다.  
  
## <a name="next-lesson"></a>다음 단원  
 [2단원: 루핑 추가](../integration-services/lesson-2-adding-looping-with-ssis.md)  
  
## <a name="see-also"></a>관련 항목  
 [프로젝트 및 패키지 실행](packages/run-integration-services-ssis-packages.md)  
  
  
