---
title: 보고서 디자이너의 식에 포함된 사용자 지정 코드 및 어셈블리 참조(SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- items [Reporting Services], expressions
- data [Reporting Services], expressions
- expressions [Reporting Services], about expressions
- expressions [Reporting Services]
- SSRS, expressions
- formulas [Reporting Services]
- data manipulation [Reporting Services]
- SQL Server Reporting Services, expressions
ms.assetid: ae8a0166-2ccc-45f4-8d28-c150da7b73de
caps.latest.revision: 76
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 6a239f80c3b560e60ca0b60b9a9fa7deb68a20a8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37220853"
---
# <a name="custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs"></a>보고서 디자이너의 식에 포함된 사용자 지정 코드 및 어셈블리 참조(SSRS)
  보고서에 포함된 사용자 지정 코드 또는 직접 작성한 사용자 지정 어셈블리에 대한 참조를 추가한 다음 컴퓨터에 저장하고 보고서 서버로 배포할 수 있습니다. 단일 보고서에서 여러 번 사용된 함수, 사용자 지정 상수 또는 복잡한 함수에는 포함 코드를 사용합니다. 코드를 한 위치에서 관리하면서 여러 보고서에서 사용할 수 있도록 공유하려면 사용자 지정 코드 어셈블리를 사용합니다. 사용자 지정 코드에는 새로운 사용자 지정 상수, 변수, 함수 또는 서브루틴이 포함될 수 있습니다. Parameters 컬렉션과 같은 기본 제공 컬렉션에 대한 읽기 전용 참조를 포함할 수 있습니다. 그러나 사용자 지정 함수에 보고서 데이터 값 집합을 전달할 수 없으며 특히 사용자 지정 집계는 지원되지 않습니다.  
  
> [!IMPORTANT]  
>  런타임에 한 번 계산되고 보고서 처리 과정에서 같은 값을 유지해야 하는 시간적 제한을 받는 계산의 경우 보고서 변수 또는 그룹 변수 사용을 고려하십시오. 자세한 내용은 [보고서 및 그룹 변수 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](built-in-collections-report-and-group-variables-references-report-builder.md)를 참조하세요.  
  
 기본적으로는 보고서 디자이너를 제작 환경으로 사용하여 보고서에 사용자 지정 코드를 추가합니다. 보고서 작성기에서는 유효한 식을 포함하거나 보고서 서버에 있는 사용자 지정 어셈블리에 대한 참조를 포함하는 보고서를 처리할 수 있습니다. 그러나 보고서 작성기에서 사용자 지정 어셈블리에 대한 참조를 추가할 수는 없습니다.  
  
> [!NOTE]  
>  보고서 서버를 업그레이드하는 동안 사용자 지정 어셈블리를 사용하는 보고서의 경우에는 업그레이드를 완료하려면 추가 단계를 수행해야 할 수 있습니다. 자세한 내용은 [Use Upgrade Advisor to Prepare for Upgrades](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RB3"></a> 보고서 작성기에서 사용자 지정 코드 작업  
 보고서 작성기에서는 사용자 지정 어셈블리에 대한 참조를 포함하는 보고서 서버의 보고서를 열 수 있습니다. 예를 들어 보고서 디자이너를 사용하여 만들고 배포한 보고서를 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 편집할 수 있습니다. 사용자 지정 어셈블리는 보고서 서버에 배포해야 합니다.  
  
 다음 작업은 수행할 수 없습니다.  
  
1.  보고서에 대한 참조 또는 클래스 멤버 인스턴스 추가  
  
2.  로컬 모드에서 사용자 지정 어셈블리에 대한 참조가 포함된 보고서 미리 보기  
  
##  <a name="Common"></a> 일반적으로 사용되는 함수에 대한 참조 포함  
 **식** 대화 상자를 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 기본 제공되는 일반적으로 사용되는 함수 목록을 범주별로 볼 수 있습니다. **일반 함수** 를 확장하고 범주를 클릭하면 식에 포함할 수 있는 함수 목록이 **항목** 창에 표시됩니다. 일반 함수에는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] <xref:System.Math> 및 <xref:System.Convert> 네임스페이스의 클래스와 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 런타임 라이브러리 함수가 포함됩니다. 편의상 **식** 대화 상자에서 범주별로 나열된 가장 일반적으로 사용되는 함수 목록을 볼 수 있습니다. 범주는 텍스트, 날짜 및 시간, 수치 연산, 검사, 프로그램 흐름, 집계, 재무, 변환 및 기타입니다. 자주 사용되지 않는 함수는 목록에 표시되지 않지만 식에 사용할 수 있습니다.  
  
 기본 제공 함수를 사용하려면 항목 창에서 함수 이름을 두 번 클릭합니다. 함수 설명이 설명 창에 표시되고 함수 호출 예가 예제 창에 표시됩니다. 코드 창에서 함수 이름을 입력하고 왼쪽 괄호 **(** 를 입력하면 IntelliSense 도움말을 통해 해당 함수 호출에 적합한 각 구문이 표시됩니다. 예를 들어 테이블의 `Quantity` 라는 필드에 대한 최대값을 계산하려면 코드 창에 `=Max(` 라는 간단한 식을 입력하고 스마트 태그를 사용하여 해당 함수 호출에 대해 유효한 모든 구문 목록을 확인합니다. 이 예를 완료하려면 `=Max(Fields!Quantity.Value)`를 입력합니다.  
  
 각 함수에 대한 자세한 내용은 <xref:System.Math>, <xref:System.Convert>및 MSDN의 [Visual Basic 런타임 라이브러리 멤버](http://go.microsoft.com/fwlink/?LinkId=198941) 를 참조하세요.  
  
##  <a name="NotCommon"></a> 일반적으로 사용되지 않는 함수에 대한 참조 포함  
 일반적으로 사용되지 않는 다른 CLR 네임스페이스에 대한 참조를 포함하려면 <xref:System.Text.StringBuilder>를 참조하세요. 일반적으로 사용되지 않는 이러한 함수의 경우 **식** 대화 상자의 코드 창에서 IntelliSense가 지원되지 않습니다.  
  
 자세한 내용은 MSDN의 [Visual Basic 런타임 라이브러리 멤버](http://go.microsoft.com/fwlink/?LinkId=198941) 를 참조하세요.  
  
##  <a name="External"></a> 외부 어셈블리에 대한 참조 포함  
 외부 어셈블리의 클래스에 대한 참조를 포함하려면 보고서 처리기에 대한 어셈블리를 확인해야 합니다. **보고서 속성** 대화 상자의 **참조** 페이지를 사용하여 보고서에 추가할 어셈블리의 정규화된 이름을 지정할 수 있습니다. 식에서 어셈블리의 클래스에 대한 정규화된 이름을 사용해야 합니다. 외부 어셈블리의 클래스는 **식** 대화 상자에 표시되지 않으므로 정확한 클래스 이름을 입력해야 합니다. 정규화된 이름에는 네임스페이스, 클래스 이름 및 멤버 이름이 포함됩니다.  
  
##  <a name="Embedded"></a> 포함 코드 포함  
 보고서에 포함 코드를 추가하려면 **보고서 속성** 대화 상자의 코드 탭을 사용합니다. 만드는 코드 블록에는 여러 메서드가 포함될 수 있습니다. 포함 코드의 메서드는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 으로 작성되고 인스턴스를 기반으로 해야 합니다. 보고서 처리기는 System.Convert 및 System.Math 네임스페이스에 대한 참조를 자동으로 추가합니다. **보고서 속성** 대화 상자의 **참조** 페이지를 사용하여 다른 어셈블리 참조를 추가할 수 있습니다. 자세한 내용은 [보고서에 어셈블리 참조 추가&#40;SSRS&#41;](add-an-assembly-reference-to-a-report-ssrs.md)를 참조하세요.  
  
 포함 코드의 메서드는 전역적으로 정의된 `Code` 멤버를 통해 사용할 수 있습니다. 참조 하 여 이러한 메서드에 액세스 합니다 `Code` 메서드 이름과 멤버입니다. 다음 예제에서는 메서드를 호출 `ToUSD`를 값으로 변환 하는 `StandardCost` 필드 값을 달러 값:  
  
```  
=Code.ToUSD(Fields!StandardCost.Value)  
```  
  
 사용자 지정 코드에서 기본 제공 컬렉션을 참조 하려면 기본 제공에 대 한 참조를 포함할 `Report` 개체:  
  
```  
=Report.Parameters!Param1.Value  
```  
  
 다음 예에서는 몇 가지 사용자 지정 상수 및 변수를 정의하는 방법을 보여 줍니다.  
  
```  
Public Const MyNote = "Authored by Bob"  
Public Const NCopies As Int32 = 2  
Public Dim  MyVersion As String = "123.456"  
Public Dim MyDoubleVersion As Double = 123.456  
```  
  
 **식** 대화 상자의 **상수** 범주에서는 기본 제공 상수만 표시되고 사용자 지정 상수는 표시되지 않지만 아래 예와 같이 식에서 사용자 지정 상수에 대한 참조를 추가할 수 있습니다. 사용자 지정 상수 취급 식에는 `Variant`합니다.  
  
```  
=Code.MyNote  
=Code.NCopies  
=Code.MyVersion  
=Code.MyDoubleVersion  
```  
  
 다음 예제 코드 참조와 함수의 코드 구현이 모두 포함 `FixSpelling`, 텍스트를 대체 하는 `"Bicycle"` 에서 "Bike" 텍스트의 모든 항목에 대 한는 `SubCategory` 필드입니다.  
  
 `=Code.FixSpelling(Fields!SubCategory.Value)`  
  
 다음 코드를 보고서 정의 코드 블록에 포함하면 `FixSpelling` 메서드의 구현을 볼 수 있습니다. 이 예제에 대 한 정규화 된 참조를 사용 하는 방법을 보여 줍니다.는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] `StringBuilder` 클래스입니다.  
  
```vb  
Public Function FixSpelling(ByVal s As String) As String  
   Dim strBuilder As New System.Text.StringBuilder(s)  
   If s.Contains("Bike") Then  
      strBuilder.Replace("Bike", "Bicycle")  
      Return strBuilder.ToString()  
      Else : Return s  
   End If  
End Function  
```  
  
 기본 제공 개체 컬렉션 및 초기화에 대한 자세한 내용은 [기본 제공 Globals 및 Users 참조&#40;보고서 작성기 및 SSRS&#41;](built-in-collections-built-in-globals-and-users-references-report-builder.md) 및 [사용자 지정 어셈블리 개체 초기화](../custom-assemblies/initializing-custom-assembly-objects.md)를 참조하세요.  
  
##  <a name="Parameters"></a> 코드에서 매개 변수에 대한 참조 포함  
 보고서 정의의 코드 블록 또는 사용자가 제공하는 사용자 지정 어셈블리에서 사용자 지정 코드를 통해 전역 매개 변수 컬렉션을 참조할 수 있습니다. 매개 변수 컬렉션은 읽기 전용이며 공개 반복기는 없습니다. 사용할 수 없습니다는 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] `For Each` 컬렉션을 단계별로 실행할을 생성 합니다. 보고서 정의에 정의된 매개 변수 이름을 알아야 사용자의 코드에서 해당 매개 변수를 참조할 수 있습니다. 하지만 다중값 매개 변수의 모든 값을 반복할 수 있습니다.  
  
 다음 표에는 사용자 지정 코드에서 기본 제공 컬렉션 `Parameters`를 참조하는 예가 들어 있습니다.  
  
|Description|식에서의 참조|사용자 지정 코드 정의|  
|-----------------|-----------------------------|----------------------------|  
|전체 전역 매개 변수 컬렉션을 사용자 지정 코드에 전달.<br /><br /> 이 함수는 특정 보고서 매개 변수 *MyParameter*의 값을 반환합니다.|`=Code.DisplayAParameterValue(Parameters)`|`Public Function DisplayAParameterValue(`<br /><br /> `ByVal parameters as Parameters) as Object`<br /><br /> `Return parameters("MyParameter").Value`<br /><br /> `End Function`|  
|개별 매개 변수를 사용자 지정 코드에 전달.<br /><br /> 이 예에서는 전달된 매개 변수의 값을 반환합니다. 매개 변수가 다중값 매개 변수일 경우 반환 문자열은 모든 값을 연결한 것입니다.|`=Code.ShowParametersValues(Parameters!DayOfTheWeek)`|`Public Function ShowParameterValues(ByVal parameter as Parameter)` <br />  `as String` <br /> `Dim s as String`  <br />  `If parameter.IsMultiValue then` <br />  `s = "Multivalue: "`  <br /> `For i as integer = 0 to parameter.Count-1` <br />  `s = s + CStr(parameter.Value(i)) + " "`  <br />  `Next` <br /> `Else` <br /> `s = "Single value: " + CStr(parameter.Value)` <br /> `End If` <br />  `Return s` <br /> `End Function`|  
  
##  <a name="Custom"></a> 사용자 지정 어셈블리에서 코드에 대한 참조 포함  
 보고서에 사용자 지정 어셈블리를 사용하려면 먼저 어셈블리를 만들고 보고서 디자이너에서 사용할 수 있게 한 다음 보고서에 어셈블리에 대한 참조를 추가하고 보고서에서 식을 사용하여 해당 어셈블리에 포함된 메서드를 참조해야 합니다. 보고서가 보고서 서버에 배포될 때 사용자 지정 어셈블리도 보고서 서버에 배포해야 합니다.  
  
 사용자 지정 어셈블리를 만들고 사용할 수 있도록 하는 방법에 대 한 자세한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 참조 하세요 [보고서를 사용 하 여 사용자 지정 어셈블리를 사용 하 여](../custom-assemblies/using-custom-assemblies-with-reports.md)입니다.  
  
 식의 사용자 지정 코드를 참조하려면 어셈블리 내에서 클래스의 멤버를 호출해야 합니다. 이 방법은 메서드가 정적인지 아니면 인스턴스 기반인지에 따라 달라집니다. 사용자 지정 어셈블리 내의 정적 메서드는 보고서 내에서 전체적으로 사용할 수 있습니다. 식에서 네임스페이스, 클래스 및 메서드 이름을 지정하여 정적 메서드에 액세스할 수 있습니다. 다음 예제에서는 메서드를 호출 `ToGBP`, 값으로 변환 하는 **StandardCost** 달러에서 파운드로 값:  
  
```  
=CurrencyConversion.DollarCurrencyConversion.ToGBP(Fields!StandardCost.Value)  
```  
  
 인스턴스 기반 메서드는 전역적으로 정의된 `Code` 멤버를 통해 사용할 수 있습니다. `Code` 멤버를 참조한 다음 인스턴스와 메서드 이름을 참조하여 이러한 메서드에 액세스합니다. 다음 예제에서는 인스턴스 메서드를 호출 `ToEUR`를 값으로 변환 하는 **StandardCost** 을 달러에서 유로로:  
  
```  
=Code.m_myDollarCoversion.ToEUR(Fields!StandardCost.Value)  
```  
  
> [!NOTE]  
>  보고서 디자이너에 사용자 지정 어셈블리를 로드하면 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]를 닫을 때까지 언로드되지 않습니다. 보고서 미리 보기를 수행할 경우 보고서에 사용된 사용자 지정 어셈블리를 변경한 다음 다시 보고서 미리 보기를 수행하면 변경 내용이 적용되어 나타나지 않습니다. 어셈블리를 다시 로드하려면 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 를 닫고 다시 연 다음 보고서 미리 보기를 수행하세요.  
  
 코드에 액세스하는 방법은 [Accessing Custom Assemblies Through Expressions](../custom-assemblies/accessing-custom-assemblies-through-expressions.md)를 참조하세요.  
  
##  <a name="collections"></a> 사용자 지정 어셈블리에 기본 제공 컬렉션 전달  
 처리 작업을 위해 *전역* 또는 *매개 변수* 컬렉션과 같은 기본 제공 컬렉션을 사용자 지정 어셈블리에 전달하려는 경우 기본 제공 컬렉션을 정의하고 올바른 네임스페이스에 액세스하는 어셈블리에 코드 프로젝트의 어셈블리 참조를 추가해야 합니다. 보고서 서버에서 실행되는 보고서(서버 보고서)에 대한 사용자 지정 어셈블리를 개발하는지, 아니면 .NET 응용 프로그램에서 로컬로 실행되는 보고서(로컬 보고서)에 대한 사용자 지정 어셈블리를 개발하는지에 따라 다른 어셈블리를 참조해야 합니다. 자세한 내용은 아래를 참조하세요.  
  
-   **네임스페이스:** Microsoft.ReportingServices.ReportProcessing.ReportObjectModel  
  
-   **어셈블리(로컬 보고서):** Microsoft.ReportingServices.ProcessingObjectModel.dll  
  
-   **어셈블리(서버 보고서):** Microsoft.ReportViewer.ProcessingObjectModel.dll  
  
 *Fields* 및 *ReportItems* 컬렉션의 내용은 런타임에 동적으로 변경될 수 있으므로 사용자 지정 어셈블리에 대한 호출에서(예: 멤버 변수) 해당 컬렉션을 유지해서는 안 됩니다. 일반적으로 모든 기본 제공 컬렉션에 같은 권장 사항이 적용됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서에 코드를 추가 &#40;SSRS&#41;](add-code-to-a-report-ssrs.md)   
 [보고서를 사용 하 여 사용자 지정 어셈블리 사용](../custom-assemblies/using-custom-assemblies-with-reports.md)   
 [보고서에 어셈블리 참조 추가&#40;SSRS&#41;](add-an-assembly-reference-to-a-report-ssrs.md)   
 [Reporting Services 자습서 &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [보고서 예제(보고서 작성기 및 SSRS)](http://go.microsoft.com/fwlink/?LinkId=198283)  
  
  
