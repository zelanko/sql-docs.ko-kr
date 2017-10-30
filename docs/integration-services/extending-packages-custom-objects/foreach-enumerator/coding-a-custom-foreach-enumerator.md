---
title: "사용자 지정 Foreach 열거자 코딩 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
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
- custom foreach enumerators [Integration Services], coding
ms.assetid: 279cf6de-d06f-40e7-b8ca-569310449f36
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 74e6e838c3dcfb18e52a8fbf460a5b71ee25399a
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="coding-a-custom-foreach-enumerator"></a>사용자 지정 Foreach 열거자 코딩
  <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator> 기본 클래스에서 상속된 클래스를 만들고 이 클래스에 <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute> 특성을 적용한 후에는 기본 클래스의 속성 및 메서드 구현을 재정의하여 사용자 지정 기능을 제공해야 합니다.  
  
 사용자 지정 열거자의 작업 예제를 참조 하십시오. [사용자 인터페이스 사용자 지정 ForEach 열거자에 대 한 개발](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-user-interface-for-a-custom-foreach-enumerator.md)합니다.  
  
## <a name="initializing-the-enumerator"></a>열거자 초기화  
 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.InitializeForEachEnumerator%2A> 메서드를 재정의하여 패키지에 정의된 연결 관리자에 대한 참조를 캐시하고 오류, 경고 및 정보 메시지를 발생시키는 데 사용할 수 있는 이벤트 인터페이스에 대한 참조를 캐시할 수 있습니다.  
  
## <a name="validating-the-enumerator"></a>열거자 유효성 검사  
 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.Validate%2A> 메서드를 재정의하여 열거자가 올바르게 구성되어 있는지 확인할 수 있습니다. 메서드에서 반환 되 면 **오류**, 열거자 및 열거자를 포함 하는 패키지 실행 되지 것입니다. 이 메서드의 구현은 각 열거자에 고유하지만 열거자가 <xref:Microsoft.SqlServer.Dts.Runtime.Variable> 또는 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 개체에 의존하는 경우 코드를 추가하여 메서드에 제공된 컬렉션에 이러한 개체가 있는지 확인해야 합니다.  
  
 다음 코드 예에서는 열거자의 속성에 지정된 변수를 확인하는 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.Validate%2A>의 구현을 보여 줍니다.  
  
```csharp  
private string variableNameValue;  
  
public string VariableName  
{  
    get{ return this.variableNameValue; }  
    set{ this.variableNameValue = value; }  
}  
  
public override DTSExecResult Validate(Connections connections, VariableDispenser variableDispenser, IDTSInfoEvents infoEvents, IDTSLogging log)  
{  
    if (!variableDispenser.Contains(this.variableNameValue))  
    {  
        infoEvents.FireError(0, "MyEnumerator", "The Variable " + this.variableNameValue + " does not exist in the collection.", "", 0);  
            return DTSExecResult.Failure;  
    }  
    return DTSExecResult.Success;  
}  
```  
  
```vb  
Private variableNameValue As String  
  
Public Property VariableName() As String  
    Get   
         Return Me.variableNameValue  
    End Get  
    Set (ByVal Value As String)   
         Me.variableNameValue = value  
    End Set  
End Property  
  
Public Overrides Function Validate(ByVal connections As Connections, ByVal variableDispenser As VariableDispenser, ByVal infoEvents As IDTSInfoEvents, ByVal log As IDTSLogging) As DTSExecResult  
    If Not variableDispenser.Contains(Me.variableNameValue) Then  
        infoEvents.FireError(0, "MyEnumerator", "The Variable " + Me.variableNameValue + " does not exist in the collection.", "", 0)  
            Return DTSExecResult.Failure  
    End If  
    Return DTSExecResult.Success  
End Function  
```  
  
## <a name="returning-the-collection"></a>컬렉션 반환  
 실행 중 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> 컨테이너는 사용자 지정 열거자의 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A> 메서드를 호출합니다. 이 메서드에서 열거자는 항목 컬렉션을 만들어 채운 다음 반환합니다. 그런 다음 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop>는 컬렉션의 항목을 반복하고 컬렉션의 각 항목에 대한 제어 흐름을 실행합니다.  
  
 다음 예에서는 난수의 배열을 반환하는 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A>의 구현을 보여 줍니다.  
  
```csharp  
public override object GetEnumerator()  
{  
    ArrayList numbers = new ArrayList();  
  
    Random randomNumber = new Random(DateTime.Now);  
  
    for( int x=0; x < 100; x++ )  
        numbers.Add( randomNumber.Next());  
  
    return numbers;  
}  
```  
  
```vb  
Public Overrides Function GetEnumerator() As Object  
    Dim numbers As ArrayList =  New ArrayList()   
  
    Dim randomNumber As Random =  New Random(DateTime.Now)   
  
        Dim x As Integer  
        For  x = 0 To  100- 1  Step  x + 1  
        numbers.Add(randomNumber.Next())  
        Next  
  
    Return numbers  
End Function  
```  
 
## <a name="see-also"></a>참고 항목  
 [사용자 지정 Foreach 열거자 만들기](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/creating-a-custom-foreach-enumerator.md)   
 [사용자 지정 ForEach 열거자에 대 한 사용자 인터페이스 개발](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-user-interface-for-a-custom-foreach-enumerator.md)  
  
  

