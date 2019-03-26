---
title: '3단계: 오류 흐름 리디렉션 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5683a45d-9e73-4cd5-83ca-fae8b26b488c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f926f1c1cb9c730401c220120c04ee679d005745
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58272006"
---
# <a name="lesson-4-3-add-error-flow-redirection"></a>4-3단원: 오류 흐름 리디렉션 추가

이전 태스크에서 변환이 오류를 생성하는 손상된 샘플 플랫 파일을 처리하려고 할 때 Lookup Currency Key 변환은 일치하는 항목을 생성할 수 없습니다. 변환은 오류 출력에 대해 기본 설정을 사용하므로 오류가 발생하면 변환이 실패합니다. 변환이 실패하면 나머지 패키지도 실패합니다.  
  
이때 변환이 실패하도록 두는 대신 오류 출력을 사용하여 실패한 행을 구성 요소가 다른 처리 경로로 리디렉션하도록 구성할 수 있습니다. 별도의 오류 처리 경로를 사용하면 더 많은 옵션이 제공됩니다. 예를 들어 데이터를 정리한 다음, 실패한 행을 다시 처리할 수 있습니다. 또는 나중에 유효성을 검사하고 다시 처리할 수 있도록 오류 정보와 함께 실패한 행을 저장할 수 있습니다.  
  
이 태스크에서는 Lookup Currency Key 변환을 구성하여 실패한 모든 행을 오류 출력으로 리디렉션합니다. 데이터 흐름의 오류 분기에서 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]는 이러한 행을 파일에 기록합니다.  
  
기본적으로 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 오류 출력의 두 개의 추가 열(**ErrorCode** 및 **ErrorColumn**)에는 숫자 오류 코드와 오류가 발생한 열의 ID만 포함되어 있습니다. 이 태스크에서는 패키지가 실패한 행을 파일에 기록하기 전에 스크립트 구성 요소를 사용하여 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] API에 액세스하고 오류 설명을 가져옵니다.  
  
## <a name="configure-an-error-output"></a>오류 출력 구성  
  
1.  **SSIS 도구 상자**에서 **일반**을 확장한 다음 **스크립트 구성 요소** 를 **데이터 흐름** 탭의 디자인 화면으로 끕니다. 이때 **스크립트** 를 **Lookup Currency Key** 변환의 오른쪽에 배치합니다.  
  
2.  **스크립트 구성 요소 유형 선택** 대화 상자에서 **변환**을 선택한 다음, **확인**을 선택합니다.  
  
3.  두 구성 요소를 연결하려면 **Lookup Currency Key** 변환을 선택한 다음, 빨간색 화살표를 새 **Script** 변환으로 끌어다 놓습니다.  
  
    빨간색 화살표는 **Lookup Currency Key** 변환의 오류 출력을 나타냅니다. 빨간색 화살표를 통해 변환을 스크립트 구성 요소에 연결하여 모든 처리 오류를 스크립트 구성 요소에 리디렉션하고, 이 구성 요소에서 오류를 처리하고, 대상으로 보냅니다.  
  
4.  **오류 출력 구성** 대화 상자의 **오류** 열에서 **행 리디렉션**을 선택한 다음, **확인**을 선택합니다.  
  
5.  **데이터 흐름** 디자인 화면에서 새 **스크립트 구성 요소**의 **스크립트 구성 요소** 이름을 선택하고 해당 이름을 **Get Error Description**으로 변경합니다.  
  
6.  **Get Error Description** 변환을 두 번 클릭합니다.  
  
7.  **스크립트 변환 편집기** 대화 상자의 **입력 열** 페이지에서 **ErrorCode** 열을 선택합니다.  
  
8.  **입/출력** 페이지에서 **출력 0**을 확장하고 **출력 열**을 선택한 다음, **열 추가**를 선택합니다.  
  
9. **Name** 속성에 *ErrorDescription*을 입력하고 **DataType** 속성을 **Unicode string [DT_WSTR]** 으로 설정합니다.  
  
10. **스크립트** 페이지에서 **LocaleID** 속성이 **영어(미국)** 로 설정되었는지 확인합니다.
  
11. **스크립트 편집**을 선택하여 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Tools for Applications(VSTA)를 엽니다. **Input0_ProcessInputRow** 메서드에 다음 코드를 입력하거나 붙여넣습니다.  
  
    [Visual Basic]  
  
    ```vb  
    Row.ErrorDescription =   
      Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
    ```  
  
    [Visual C#]  
  
    ```cs
    Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
    ```  
  
    완성된 서브루틴은 다음 코드와 같습니다.  
  
    [Visual Basic]  
  
    ```vb
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
      Row.ErrorDescription =   
        Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
  
    End Sub  
    ```  
  
    [Visual C#]  
  
    ```cs
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
        {  
  
            Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
  
        }  
    ```  
  
12. **빌드** 메뉴에서 **솔루션 빌드**를 선택하여 스크립트를 빌드하고 변경 내용을 저장한 다음, VSTA를 닫습니다.  
  
13. **확인**을 선택하여 **스크립트 변환 편집기** 대화 상자를 닫습니다.  
  
## <a name="go-to-next-task"></a>다음 작업으로 이동
[4단계: 플랫 파일 대상 추가](../integration-services/lesson-4-4-adding-a-flat-file-destination.md)  
  
  
  
