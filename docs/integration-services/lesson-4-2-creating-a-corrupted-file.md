---
title: '2단계: 손상된 파일 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: cd0b18dc-66c3-4d88-86ef-8e40cb660fae
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9805a1d1fd1c6e025ee7ddb83c7241037dbae30b
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58273359"
---
# <a name="lesson-4-2-create-a-corrupted-file"></a>4-2단원: 손상된 파일 만들기

변환 오류의 구성 및 처리를 보여주기 위해 처리 시 구성 요소의 실패를 야기하는 샘플 플랫 파일이 필요합니다.  
  
이 태스크에서는 기존 샘플 플랫 파일의 복사본을 만듭니다. 그런 다음, 메모장에서 파일을 열고 잘못된 값을 포함하도록 **CurrencyID** 열을 편집하면 조회가 실패합니다. 이 손상된 파일을 처리하면 조회 실패로 Currency Key Lookup 변환이 실패하며 따라서 패키지의 나머지 부분도 실패합니다. 손상된 샘플 파일을 만든 후에 패키지를 실행하여 패키지 오류를 봅니다.  
  
## <a name="create-a-corrupted-sample-flat-file"></a>손상된 샘플 플랫 파일 만들기  
  
1.  메모장이나 기타 텍스트 편집기에서 **Currency_VEB.txt** 파일을 엽니다.  
  
2.  텍스트 편집기의 찾기 및 바꾸기 기능을 사용하여 모든 **VEB** 인스턴스를 찾은 다음 모두 **BAD**로 바꿉니다.  
  
3.  다른 샘플 데이터 파일과 동일한 폴더에서 수정된 파일을 **Currency_BAD.txt**로 저장합니다.  
  
    > [!NOTE]  
    > **Currency_BAD.txt**를 다른 샘플 데이터 파일과 동일한 폴더에 저장했는지 확인합니다.  
  
4.  텍스트 편집기를 닫습니다.  
  
## <a name="verify-that-an-error-occurs-during-run-time"></a>런타임 중에 오류가 발생하는지 확인  
  
1.  **디버그** 메뉴에서 **디버깅 시작**을 선택합니다.  
  
    세 번째 데이터 흐름 반복에서 Lookup Currency Key 변환은 **Currency_BAD.txt** 파일을 처리하려고 하며 여기서 변환이 실패합니다. 변환 실패로 인해 전체 패키지가 실패하게 됩니다.  
  
2.  **디버그** 메뉴에서 **디버깅 중지**를 선택합니다.  
  
3.  디자인 화면에서 **실행 결과** 탭을 선택합니다.  
  
4.  로그를 찾아보고 다음의 처리되지 않은 오류가 발생했는지 확인합니다.  
  
    ```
    [Lookup Currency Key[27]] Error: Row yielded no match during lookup.
    ```
  
    > [!NOTE]  
    > 27은 구성 요소의 ID입니다. 이 값은 데이터 흐름을 작성할 때 할당되며 패키지 값과 다를 수 있습니다.  
  
## <a name="go-to-next-task"></a>다음 작업으로 이동  
[3단계: 오류 흐름 리디렉션 추가](../integration-services/lesson-4-3-adding-error-flow-redirection.md)  
  
  
  
