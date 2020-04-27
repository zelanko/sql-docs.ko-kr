---
title: '3단계: 오류 흐름 리디렉션 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5683a45d-9e73-4cd5-83ca-fae8b26b488c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3dd2fd95b1ad2d239d055b2b49b991860a58d338
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62891405"
---
# <a name="step-3-adding-error-flow-redirection"></a>3단계: 오류 Flow 리디렉션 추가
  이전 태스크에서 설명한 대로 Lookup Currency Key 변환은 오류를 생성한 손상된 예제 플랫 파일을 처리할 때 일치하는 항목을 생성할 수 없습니다. 변환은 오류 출력에 대해 기본 설정을 사용하므로 오류가 발생하면 변환이 실패합니다. 변환이 실패하면 나머지 패키지도 실패합니다.  
  
 이때 변환이 실패하도록 두는 대신 오류 출력을 사용하여 실패한 행을 구성 요소가 다른 처리 경로로 리디렉션하도록 구성할 수 있습니다. 별도의 오류 처리 경로를 사용하면 다양한 작업을 수행할 수 있습니다. 예를 들어 데이터를 정리한 다음 실패한 행을 다시 처리하거나 나중에 유효성을 검사하고 다시 처리할 수 있도록 추가 오류 정보와 함께 실패한 행을 저장할 수 있습니다.  
  
 이 태스크에서는 Lookup Currency Key 변환을 구성하여 실패하는 모든 행을 오류 출력으로 리디렉션합니다. 이러한 행은 데이터 흐름의 오류 분기에서 파일에 기록됩니다.  
  
 기본적으로 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 오류 출력의 추가 열인 **ErrorCode** 및 **errorcolumn**에는 오류 번호를 나타내는 숫자 코드와 오류가 발생 한 열의 ID만 포함 됩니다. 이러한 숫자 값은 해당 오류 설명이 없으므로 사용이 제한적일 수 있습니다.  
  
 실패한 행을 패키지가 파일에 기록하기 전에 스크립트 구성 요소를 사용하여 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] API에 액세스한 다음 오류 설명을 가져와 오류 출력의 유용성을 향상시킬 수 있습니다.  
  
### <a name="to-configure-an-error-output"></a>오류 출력을 구성하려면  
  
1.  **SSIS 도구 상자**에서 **일반**을 확장 한 다음 **스크립트 구성 요소** 를 **데이터 흐름** 탭의 디자인 화면으로 끌어다 놓습니다. **Lookup Currency Key** 변환의 오른쪽에 **스크립트** 를 배치 합니다.  
  
2.  **스크립트 구성 요소 유형 선택** 대화 상자에서 **변환**을 클릭한 다음 **확인**을 클릭합니다.  
  
3.  **Lookup Currency Key** 변환을 클릭하고 빨간색 화살표를 새로 추가한 **Script** 변환으로 끌어 두 구성 요소를 연결합니다.  
  
     빨간색 화살표는 **Lookup Currency Key** 변환의 오류 출력을 나타냅니다. 빨간색 화살표를 통해 변환을 스크립트 구성 요소에 연결하여 모든 처리 오류를 스크립트 구성 요소에 리디렉션한 다음 이 구성 요소에서 오류를 처리하고 대상에 보내도록 할 수 있습니다.  
  
4.  **오류 출력 구성** 대화 상자의 **오류** 열에서 **행 리디렉션**을 선택한 다음 **확인**을 클릭합니다.  
  
5.  **데이터 흐름** 디자인 화면에서 새로 추가한 **스크립트 구성 요소** 의 **스크립트 구성 요소**를 클릭한 다음 이름을 **Get Error Description**으로 변경합니다.  
  
6.  **Get Error Description** 변환을 두 번 클릭합니다.  
  
7.  **스크립트 변환 편집기** 대화 상자의 **입력 열** 페이지에서 **ErrorCode** 열을 선택합니다.  
  
8.  **입/출력** 페이지에서 **출력 0**을 확장하고 **출력 열**을 클릭한 다음 **열 추가**를 클릭합니다.  
  
9. 속성에 **ErrorDescription** 을 `DataType` 입력 하 고 속성을 **유니코드 문자열 [DT_WSTR]** 로 설정 합니다. `Name`  
  
10. **스크립트** 페이지에서 `LocaleID` 속성이 **영어 (미국)** 로 설정 되어 있는지 확인 합니다.  
  
11. **스크립트 편집**을 클릭하여 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] VSTA(Tools for Applications)를 엽니다. `Input0_ProcessInputRow` 메서드에 다음 코드를 입력하거나 붙여 넣습니다.  
  
     [Visual Basic]  
  
    ```  
    Row.ErrorDescription =   
      Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
    ```  
  
     [Visual C#]  
  
    ```  
    Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
    ```  
  
     완성된 서브루틴은 다음 코드와 같습니다.  
  
     [Visual Basic]  
  
    ```  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
      Row.ErrorDescription =   
        Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
  
    End Sub  
    ```  
  
     [Visual C#]  
  
    ```  
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
        {  
  
            Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
  
        }  
    ```  
  
12. **빌드** 메뉴에서 **솔루션 빌드** 를 클릭하여 스크립트를 빌드하고 변경 내용을 저장한 다음 VSTA를 닫습니다.  
  
13. **확인** 을 클릭하여 **스크립트 변환 편집기** 대화 상자를 닫습니다.  
  
## <a name="next-steps"></a>다음 단계  
 [4 단계: 플랫 파일 대상 추가] (lesson-4-4-adding-a-flat-file-destination.md  
  
  
