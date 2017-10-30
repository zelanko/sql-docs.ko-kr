---
title: Enhancing an Error Output with the Script Component | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
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
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 3881b57f4089dbb075d019f9bd1a88a96a307b72
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="enhancing-an-error-output-with-the-script-component"></a>스크립트 구성 요소를 사용하여 오류 출력 향상
  기본적으로 두 개의 추가 열에는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ErrorCode 및 ErrorColumn 오류 출력을 나타내는 숫자 코드 오류 번호와 오류가 발생 한 열의 ID만 포함 합니다. 이러한 숫자 값은 해당 오류 설명과 열 이름이 없으므로 사용이 제한적일된 수 있습니다.  
  
 이 항목에서는 스크립트 구성 요소를 사용 하 여 데이터 흐름의 기존 오류 출력 데이터는 오류 설명과 열 이름을 추가 하는 방법에 설명 합니다. 예에서는 스크립트 구성 요소의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> 속성을 통해 사용할 수 있는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 인터페이스의 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> 메서드를 사용하여 미리 정의된 특정 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 오류 코드에 해당하는 오류 설명을 추가합니다. 다음 예제에서는 캡처된 계보 ID에 해당 하는 열 이름을 사용 하 여 추가 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130.GetIdentificationStringByID%2A> 동일한 인터페이스의 메서드입니다.  
  
> [!NOTE]  
>  여러 데이터 흐름 태스크 및 여러 패키지에서 쉽게 다시 사용할 수 있는 구성 요소를 만들려면 이 스크립트 구성 요소 예제에 있는 코드를 바탕으로 사용자 지정 데이터 흐름 구성 요소를 만들어 보십시오. 자세한 내용은 [사용자 지정 데이터 흐름 구성 요소 개발](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 여기에 표시 된 예에서는 변환으로 구성 된 스크립트 구성 요소를 사용 하 여 데이터 흐름의 기존 오류 출력 데이터에 오류 설명과 열 이름을 추가 합니다.  
  
 데이터 흐름의 변환으로 사용 하기 위해 스크립트 구성 요소를 구성 하는 방법에 대 한 자세한 내용은 참조 [스크립트 구성 요소를 사용 하 여 동기 변환 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md) 및 [스크립트 구성 요소를 사용 하 여 비동기 변환 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)합니다.  
  
#### <a name="to-configure-this-script-component-example"></a>스크립트 구성 요소 예를 구성하려면  
  
1.  새 스크립트 구성 요소를 만들기 전에 데이터 흐름의 업스트림 구성 요소에서 오류 또는 잘림이 발생할 경우 행을 오류 출력으로 리디렉션하도록 구성합니다. 테스트를 위해 오류가 발생하도록 구성 요소를 구성할 수 있습니다. 예를 들어 조회를 수행할 수 없는 두 테이블 간에 조회 변환을 구성할 수 있습니다.  
  
2.  데이터 흐름 디자이너 화면에 새 스크립트 구성 요소를 추가하고 이 구성 요소를 변환으로 구성합니다.  
  
3.  업스트림 구성 요소의 오류 출력을 새 스크립트 구성 요소에 연결합니다.  
  
4.  열기는 **스크립트 변환 편집기**, 및는 **스크립트** 페이지에 대 한는 **u a g e** 속성을 스크립트 언어를 선택 합니다.  
  
5.  클릭 **스크립트 편집** 열려는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSTA Tools for Applications () IDE 아래 표시 된 예제 코드를 추가 합니다.  
  
6.  VSTA를 닫습니다.  
  
7.  스크립트 변환 편집기에서에 **입력 열** 페이지에서 ErrorCode 및 ErrorColumn 열을 선택 합니다.  
  
8.  에 **입 / 출력** 페이지에서 새 열 두 개를 추가 합니다.  
  
    -   형식의 새 출력 열을 추가 **문자열** 라는 **ErrorDescription**합니다. 긴 메시지를 지원할 수 있도록 새 열의 기본 길이를 255로 늘립니다.  
  
    -   형식의 새 출력 열을 다른 추가 **문자열** 라는 **ColumnName**합니다. 긴 값을 지원 하기 위해 255 새 열의 기본 길이 늘립니다.  
  
9. 닫기는 **스크립트 변환 편집기입니다.**  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)   
 [데이터 흐름 구성 요소의 오류 출력을 사용 하 여](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)   
 [스크립트 구성 요소를 사용 하 여 동기 변환 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
  
  

