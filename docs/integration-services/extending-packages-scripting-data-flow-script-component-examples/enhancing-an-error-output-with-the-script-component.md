---
title: 스크립트 구성 요소를 사용하여 오류 출력 향상 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- transformations [Integration Services], components
- Script component [Integration Services], examples
- error outputs [Integration Services], enhancing
- Script component [Integration Services], transformation components
ms.assetid: f7c02709-f1fa-4ebd-b255-dc8b81feeaa5
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f7f310cc4260bfc621436778d6363dc8cb8276b3
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35406375"
---
# <a name="enhancing-an-error-output-with-the-script-component"></a>스크립트 구성 요소를 사용하여 오류 출력 향상
  기본적으로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 오류 출력의 추가 열인 ErrorCode 및 ErrorColumn에는 오류 번호를 나타내는 숫자 코드와 오류가 발생한 열의 ID만 포함됩니다. 이러한 숫자 값은 해당 오류 설명과 열 이름이 없으므로 사용이 제한될 수 있습니다.  
  
 이 항목에서는 스크립트 구성 요소를 사용하여 데이터 흐름의 기존 오류 출력 데이터에 오류 설명 및 열 이름을 추가하는 방법을 설명합니다. 예에서는 스크립트 구성 요소의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> 속성을 통해 사용할 수 있는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 인터페이스의 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> 메서드를 사용하여 미리 정의된 특정 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 오류 코드에 해당하는 오류 설명을 추가합니다. 그런 후 예제에서는 동일한 인터페이스의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130.GetIdentificationStringByID%2A> 메서드를 사용하여 캡처된 계보 ID에 해당하는 열 이름을 추가합니다.  
  
> [!NOTE]  
>  여러 데이터 흐름 태스크 및 여러 패키지에서 쉽게 다시 사용할 수 있는 구성 요소를 만들려면 이 스크립트 구성 요소 예제에 있는 코드를 바탕으로 사용자 지정 데이터 흐름 구성 요소를 만들어 보십시오. 자세한 내용은 [사용자 지정 데이터 흐름 구성 요소 개발](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 이 예에서는 변환으로 구성된 스크립트 구성 요소를 사용하여 데이터 흐름의 기존 오류 출력 데이터에 오류 설명 및 열 이름을 추가합니다.  
  
 데이터 흐름에서 변환으로 사용하도록 스크립트 구성 요소를 구성하는 방법에 대한 자세한 내용은 [스크립트 구성 요소를 사용하여 동기 변환 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md) 및 [스크립트 구성 요소를 사용하여 비동기 변환 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)를 참조하세요.  
  
#### <a name="to-configure-this-script-component-example"></a>스크립트 구성 요소 예를 구성하려면  
  
1.  새 스크립트 구성 요소를 만들기 전에 데이터 흐름의 업스트림 구성 요소에서 오류 또는 잘림이 발생할 경우 행을 오류 출력으로 리디렉션하도록 구성합니다. 테스트를 위해 오류가 발생하도록 구성 요소를 구성할 수 있습니다. 예를 들어 조회를 수행할 수 없는 두 테이블 간에 조회 변환을 구성할 수 있습니다.  
  
2.  데이터 흐름 디자이너 화면에 새 스크립트 구성 요소를 추가하고 이 구성 요소를 변환으로 구성합니다.  
  
3.  업스트림 구성 요소의 오류 출력을 새 스크립트 구성 요소에 연결합니다.  
  
4.  **스크립트 변환 편집기**를 열고 **스크립트** 페이지의 **ScriptLanguage** 속성에서 스크립트 언어를 선택합니다.  
  
5.  **스크립트 편집**을 클릭하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSTA(Tools for Applications) IDE를 열고 아래에 표시된 샘플 코드를 추가합니다.  
  
6.  VSTA를 닫습니다.  
  
7.  스크립트 변환 편집기의 **입력 열** 페이지에서 ErrorCode 및 ErrorColumn 열을 선택합니다.  
  
8.  **입/출력** 페이지에서 열 두 개를 새로 추가합니다.  
  
    -   **ErrorDescription**이라는 **문자열** 형식의 새 출력 열을 추가합니다. 긴 메시지를 지원할 수 있도록 새 열의 기본 길이를 255로 늘립니다.  
  
    -   **ColumnName**이라는 **문자열** 형식의 또 다른 새 출력 열을 추가합니다. 긴 값을 지원할 수 있도록 새 열의 기본 길이를 255로 늘립니다.  
  
9. **스크립트 변환 편집기**를 닫습니다.  
  
10. 스크립트 구성 요소의 출력을 적절한 대상에 연결합니다. 임시 테스트용으로 구성하는 데는 플랫 파일 대상이 가장 쉽습니다.  
  
11. 패키지를 실행합니다.  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
      Row.ErrorDescription = _  
        Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
  
      Dim componentMetaData130 = TryCast(Me.ComponentMetaData, IDTSComponentMetaData130)  
      If componentMetaData130 IsNot Nothing Then  
        Row.ColumnName = componentMetaData130.GetIdentificationStringByID(Row.ErrorColumn)  
         End If  
  
    End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
{  
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
  
      Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
  
      var componentMetaData130 = this.ComponentMetaData as IDTSComponentMetaData130;  
      if (componentMetaData130 != null)  
        {  
            Row.ColumnName = componentMetaData130.GetIdentificationStringByID(Row.ErrorColumn);  
        }  
  
    }  
}  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)   
 [데이터 흐름 구성 요소에서 오류 출력 사용](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)   
 [스크립트 구성 요소를 사용하여 동기 변환 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
  
  
