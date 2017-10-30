---
title: "스크립트 구성 요소에 대 한 오류 출력 시뮬레이션 | Microsoft Docs"
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
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], error output
- error outputs [Integration Services], Script component
ms.assetid: f8b6ecff-ac99-4231-a0e7-7ce4ad76bad0
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 0af8434531660958557928376cf8a4fd19ca9e68
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="simulating-an-error-output-for-the-script-component"></a>스크립트 구성 요소의 오류 출력 시뮬레이션
  오류 행의 자동 처리를 위해 스크립트 구성 요소의 출력을 오류 출력으로 직접 구성할 수는 없지만 적절할 때 추가 출력을 만들고 스크립트에 조건부 논리를 사용하여 행을 이 출력으로 전송하는 방식으로 기본 제공 오류 출력의 기능을 재현할 수 있습니다. 오류 번호와 오류가 발생한 열의 ID를 받는 두 개의 출력 열을 추가하여 기본 제공 오류 출력의 동작을 시뮬레이션할 수 있습니다.  
  
 미리 정의된 특정 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 오류 코드에 해당하는 오류 설명을 추가하려면 스크립트 구성 요소의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> 속성을 통해 사용할 수 있는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 인터페이스의 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> 메서드를 사용합니다.  
  
## <a name="example"></a>예제  
 이 예에서는 두 개의 동기 출력을 사용하는 변환으로 구성된 스크립트 구성 요소를 사용합니다. 이 스크립트 구성 요소의 목적은 AdventureWorks 예제 데이터베이스의 주소 데이터에서 오류 행을 필터링하는 것입니다. 이 가상 예에서는 북아메리카 고객을 대상으로 홍보 행사를 준비 중이므로 필터를 사용하여 북아메리카에 위치하지 않은 주소를 제외해야 한다고 가정합니다.  
  
#### <a name="to-configure-the-example"></a>예를 구성하려면  
  
1.  새 스크립트 구성 요소를 만들기 전에 연결 관리자를 만들고 AdventureWorks 예제 데이터베이스에서 주소 데이터를 선택하도록 데이터 흐름 원본을 구성합니다. CountryRegionName 열만 확인하는 이 예의 경우 단순히 Person.vStateCountryProvinceRegion 뷰를 사용해도 되고, Person.Address, Person.StateProvince 및 Person.CountryRegion 테이블을 조인하여 데이터를 선택해도 됩니다.  
  
2.  데이터 흐름 디자이너 화면에 새 스크립트 구성 요소를 추가하고 이 구성 요소를 변환으로 구성합니다. 열기는 **스크립트 변환 편집기**합니다.  
  
3.  에 **스크립트** 페이지에서 설정는 **u a g e** 속성을 스크립트를 코딩 하는 데 사용할 스크립트 언어입니다.  
  
4.  **스크립트 편집** 을 클릭하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications)를 엽니다.  
  
5.  에 **Input0_ProcessInputRow** 메서드를 입력 하거나 아래 표시 된 예제 코드를 붙여 넣습니다.  
  
6.  VSTA를 닫습니다.  
  
7.  에 **입력 열** 페이지에서 열을 스크립트 변환에서 처리 하려면 선택 합니다. 이 예에서는 CountryRegionName 열만 사용합니다. 사용 가능한 입력 열 중 선택하지 않은 열은 데이터 흐름에서 변경되지 않은 상태로 전달됩니다.  
  
8.  에 **입 / 출력** 페이지, 새 추가 하 고, 두 번째 출력 설정 해당 **SynchronousInputID** 값은 입력의 ID 값의는 **SynchronousInputID** 기본 출력의 속성입니다. 설정의 **ExclusionGroup** 를 나타내는 각 행을 두 출력 중 하나로 그러면 동일한 0이 아닌 값 (예: 1) 출력 모두의 속성입니다. 새 오류 출력에 "MyErrorOutput"과 같이 알기 쉬운 이름을 지정합니다.  
  
9. 오류 코드, 오류가 발생한 열의 ID, 오류 설명 등 원하는 오류 정보를 캡처하는 출력 열을 새 오류 출력에 추가합니다. 이 예에서는 ErrorColumn 및 ErrorMessage라는 새 열을 만듭니다. 개발자 고유의 구현에서 미리 정의된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 오류를 catch하려는 경우 오류 번호에 대한 ErrorCode 열을 추가해야 합니다.  
  
10. 입력 열의 ID 값은 스크립트 구성 요소에서 오류 조건을 확인하는 데 사용합니다. 이 예에서는 이 열 식별자를 사용하여 ErrorColumn 값을 채웁니다.  
  
11. 닫기는 **스크립트 변환 편집기입니다.**  
  
12. 스크립트 구성 요소의 출력을 적절한 대상에 연결합니다. 임시 테스트용으로 구성하는 데는 플랫 파일 대상이 가장 쉽습니다.  
  
13. 패키지를 실행합니다.  
  
```vb  
Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
  If Row.CountryRegionName <> "Canada" _  
      And Row.CountryRegionName <> "United States" Then  
  
    Row.ErrorColumn = 68 ' ID of CountryRegionName column  
    Row.ErrorMessage = "Address is not in North America."  
    Row.DirectRowToMyErrorOutput()  
  
  Else  
  
    Row.DirectRowToOutput0()  
  
  End If  
  
End Sub  
```  
  
```csharp  
public override void Input0_ProcessInputRow(Input0Buffer Row)  
{  
  
  if (Row.CountryRegionName!="Canada"&&Row.CountryRegionName!="United States")  
  
  {  
    Row.ErrorColumn = 68; // ID of CountryRegionName column  
    Row.ErrorMessage = "Address is not in North America.";  
    Row.DirectRowToMyErrorOutput();  
  
  }  
  else  
  {  
  
    Row.DirectRowToOutput0();  
  
  }  
  
}  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)   
 [데이터 흐름 구성 요소의 오류 출력을 사용 하 여](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)   
 [스크립트 구성 요소를 사용 하 여 동기 변환 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)  
  
  

