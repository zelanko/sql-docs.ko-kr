---
title: '5단계: 4단원 자습서 패키지 테스트 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5f18df92-0248-4858-836b-c8b02f0e0439
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 921928f48f3730353575dac9f04d0584c28c769d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37269089"
---
# <a name="step-5-testing-the-lesson-4-tutorial-package"></a>5단계: 4단원 자습서 패키지 테스트
  런타임에 손상된 파일인 Currency_BAD.txt가 있으면 Currency Key Lookup 변환에서 일치 항목을 생성하지 못합니다. 이제 Currency Key Lookup의 오류 출력이 실패한 행을 새 실패한 행 대상으로 리디렉션하도록 구성되었으므로 해당 구성 요소가 실패하지 않으며 패키지가 성공적으로 실행됩니다. 실패한 모든 오류 행은 ErrorOutput.txt에 기록됩니다.  
  
 이 태스크에서는 패키지를 실행하여 수정된 오류 출력 구성을 테스트한 다음 패키지 실행 성공 여부에 따라 ErrorOutput.txt 파일의 내용을 표시하는 방법에 대해 설명합니다.  
  
> [!NOTE]  
>  ErrorOutput.txt 파일에 오류 행이 누적되지 않도록 하려면 패키지 실행 사이에 파일 내용을 직접 삭제해야 합니다.  
  
## <a name="checking-the-package-layout"></a>패키지 레이아웃 확인  
 패키지를 테스트하려면 먼저 4단원 패키지의 제어 흐름과 데이터 흐름에 다음 다이어그램에 표시된 개체가 있는지 확인해야 합니다. 제어 흐름은 2-4단원의 제어 흐름과 동일해야 합니다.  
  
 **제어 흐름**  
  
 ![패키지의 제어 흐름](../../2014/tutorials/media/task4lesson2control.gif "패키지의 제어 흐름")  
  
 **데이터 흐름**  
  
 ![패키지의 데이터 흐름](../../2014/tutorials/media/task5lesson5data.gif "패키지의 데이터 흐름")  
  
### <a name="to-run-the-lesson-4-tutorial-package"></a>4단원 자습서 패키지를 실행하려면  
  
1.  **디버그** 메뉴에서 **디버깅 시작**을 클릭합니다.  
  
2.  패키지의 실행이 완료된 후에 **디버그** 메뉴에서 **디버깅 중지**를 클릭합니다.  
  
### <a name="to-verify-the-contents-of-the-erroroutputtxt-file"></a>ErrorOutput.txt 파일의 내용을 확인하려면  
  
-   메모장이나 텍스트 편집기에서 ErrorOutput.txt 파일을 엽니다. 기본 열 순서는 AverageRate, CurrencyID, CurrencyDate, EndOfDateRate, ErrorCode, ErrorColumn, ErrorDescription입니다.  
  
     파일의 모든 행에 일치하지 않는 CurrencyID 값인 BAD, ErrorCode 값인 -1071607778, ErrorColumn 값인 0 및 ErrorDescription 값인 "조회 중에 행에서 일치하는 항목을 생성하지 않았습니다"가 포함됩니다. 열 관련 오류가 아니라 조회 작업 오류이므로 ErrorColumn 값은 0으로 설정됩니다. 의 인스턴스에 액세스할 때마다 SQL Server 로그인을 제공할 필요가 없습니다.  
  
  
