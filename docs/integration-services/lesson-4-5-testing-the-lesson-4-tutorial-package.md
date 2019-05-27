---
title: '5단계: 4단원 자습서 패키지 테스트 | Microsoft Docs'
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5f18df92-0248-4858-836b-c8b02f0e0439
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f1c7ec3026050181ae31150c4b5e190a65d889d4
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65721513"
---
# <a name="lesson-4-5-test-the-lesson-4-package"></a>4-5단원: 4단원 패키지 테스트

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



런타임 시 손상된 파일인 **Currency_BAD.txt**는 Currency Key Lookup 변환에서 일치 항목을 생성하지 못합니다. Currency Key Lookup의 오류 출력을 구성하여 실패한 행을 새 실패한 행 대상으로 리디렉션했으므로 해당 구성 요소가 실패하지 않고 패키지가 성공적으로 실행됩니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]가 실패한 모든 오류 행을 **ErrorOutput.txt**에 기록합니다.  
  
이 태스크에서는 패키지를 실행하여 수정된 오류 출력 구성을 테스트합니다. 패키지 실행에 성공한 **ErrorOutput.txt** 파일의 내용을 표시합니다.  
  
> [!NOTE]  
> **ErrorOutput.txt** 파일에 오류 행이 누적되지 않도록 하려면 패키지 실행 사이에 파일 내용을 수동으로 삭제합니다.  
  
## <a name="check-the-package-layout"></a>패키지 레이아웃 확인  
패키지를 테스트하려면 먼저 4단원 패키지의 제어 흐름과 데이터 흐름이 다음 다이어그램과 유사한지 확인합니다. 
  
**제어 흐름**  
  
![패키지의 제어 흐름](../integration-services/media/task4lesson2control.gif "패키지의 제어 흐름")  
  
**데이터 흐름**  
  
![패키지의 데이터 흐름](../integration-services/media/task5lesson5data.gif "패키지의 데이터 흐름")  
  
## <a name="run-the-lesson-4-tutorial-package"></a>4단원 자습서 패키지 실행  
  
1.  **디버그** 메뉴에서 **디버깅 시작**을 선택합니다.  
  
2.  패키지의 실행이 완료된 후에 **디버그** 메뉴에서 **디버깅 중지**를 선택합니다.  
  
## <a name="view-the-contents-of-the-erroroutputtxt-file"></a>ErrorOutput.txt 파일 내용 보기  
  
메모장이나 텍스트 편집기에서 **ErrorOutput.txt** 파일을 엽니다. 기본 열 순서는 AverageRate, CurrencyID, CurrencyDate, EndOfDateRate, ErrorCode, ErrorColumn, ErrorDescription입니다.  
 
파일의 모든 행에 일치하지 않는 CurrencyID 값 "BAD", ErrorCode 값 -1071607778, ErrorColumn 값 0 및 ErrorDescription 값 "조회 중에 행에서 일치하는 항목을 생성하지 않았습니다"가 포함됩니다. ErrorColumn 값은 열 관련 오류가 아닌기 때문에 0입니다. 대신 조회 작업이 실패했습니다.
  
  
## <a name="next-lesson"></a>다음 단원
[5단원: 패키지 배포 모델을 위한 SSIS 패키지 구성 추가](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
