---
title: Microsoft OLE DB 단순 공급자 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- simple provider [ADO]
- providers [ADO], OLE DB simple provider
- OLE DB simple provider [ADO]
ms.assetid: 1e7dc6f0-482c-4103-8187-f890865e40fc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 33858c9cc0778e550bf90f574e4443dff033c5d1
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53209059"
---
# <a name="microsoft-ole-db-simple-provider-overview"></a>Microsoft OLE DB 단순 공급자 개요
Microsoft OLE DB 단순 공급자 (OSP)는 공급자에 기록 된 사용 하 여 모든 데이터에 액세스 하는 ADO를 허용 합니다 [OLE DB 단순 공급자 (OSP) 도구 키트](https://msdn.microsoft.com/6e7b7931-9e4a-4151-ae51-672abd3f84a6)합니다. 간단한 공급자는 메모리 내 배열 또는 XML 문서와 같은 기본만 OLE DB 지원 해야 하는 데이터 원본에 액세스 하기 위해서입니다.

## <a name="connection-string-parameters"></a>연결 문자열 매개 변수
 OLE DB 단순 공급자 DLL에 연결 하려면 다음을 설정 합니다 *공급자* 인수를 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성을:

```vb
MSDAOSP
```

 이 값을 설정 하거나 사용 하 여 읽을 수도 있습니다는 [공급자](../../../ado/reference/ado-api/provider-property-ado.md) 속성입니다.

 공급자 기록기에 의해 결정 된 등록 된 공급자 이름을 사용 하 여 전체 OLE DB 공급자로 등록 된 간단한 공급자에 연결할 수 있습니다.

## <a name="typical-connection-string"></a>일반적인 연결 문자열
 이 공급자에 대 한 일반적인 연결 문자열은:

```vb
"Provider=MSDAOSP;Data Source=serverName"
```

 문자열을 이러한 키워드 이루어져 있습니다.

|키워드|설명|
|-------------|-----------------|
|**공급자**|SQL Server 용 OLE DB 공급자를 지정합니다.|
|**데이터 원본**|서버의 이름을 지정합니다.|

## <a name="xml-document-example"></a>XML 문서 예제
 OLE DB 단순 공급자 (OSP) MDAC 2.7에서 이상 및 Windows Data Access Components (Windows DAC)을 계층적 ADO 열기를 지원 하도록 향상 되었습니다 **레코드 집합** 임의의 XML 파일입니다. 이러한 XML 파일에는 ADO XML 지 속성 스키마에 있을 수 있지만 필요 하지 않습니다. 이를 OSP를 연결 하 여 구현 되었습니다 합니다 **MSXML2.DLL**하므로 **MSXML2.DLL** 이상 버전이 필요 합니다.

 합니다 **portfolio.xml** 다음 트리를 포함 하는 다음 예제에서 사용 되는 파일:

```console
Portfolio
   Stock
      Shares
      Symbol
      Price
      Info
         Company Name
         WebSite
```

 XML DSO에서 기본 제공 추론을 사용 하 여 장에 계층적 XML 트리의 노드를 변환할 **레코드 집합**합니다.

 이러한 기본 제공 추론을 사용 하 여, XML 트리는 두 수준의 계층으로 변환 됩니다 **레코드 집합** 다음 폼의:

```console
Parent Recordset
Shares, Symbol, Price, $Text
   Child Recordset
      Company Name, WebSite, $Text
```

 포트폴리오 및 정보 태그는 계층적 표현 되지 않는 유의 **레코드 집합**합니다. XML DSO 계층적 XML 트리를 변환 하는 방법에 대 한 설명은 **레코드 집합**, 다음 규칙을 참조 하세요. $Text 열은 다음 섹션에 설명 되어 있습니다.

## <a name="rules-for-assigning-xml-elements-and-attributes-to-columns-and-rows"></a>열과 행에 할당 XML 요소와 특성에 대 한 규칙
 XML DSO 요소를 할당 하기 위한 절차 다음에 나오는 및 데이터 바인딩된 응용 프로그램에서 행 및 열에 특성. XML 트리 전체 계층 구조를 포함 하는 하나의 태그를 사용 하 여 모델링 됩니다. 예를 들어, 책에 대 한 XML 설명을 장 태그, 그림 태그 및 태그 섹션을 포함할 수 있습니다. 최상위 수준 것 하위 장, 그림 및 섹션을 포함 하는 책 태그입니다. XML DSO 행 및 열에 XML 요소를 맵, 최상위 수준 요소가 아닌 하위 요소 변환 됩니다.

 XML DSO 하위 요소를 변환 하는 데이 절차를 사용 합니다.

-   일부 열에 해당 하는 각 하위 요소와 특성 **레코드 집합** 계층 구조에서.

-   열의 이름은 하위 요소 또는 특성의 이름과 동일 경우 부모 요소에 특성 및 동일한 이름 가진 하위 요소는 "!" 하위의 열 이름 앞에 추가 됩니다.

-   각 열은는 *단순* 스칼라 값 (일반적으로 문자열)를 포함 하는 열 또는 **레코드 집합** 자식을 포함 하는 열 **레코드 집합**합니다.

-   특성에 해당 하는 열 도형은 항상 단순 합니다.

-   하위 요소에 해당 하는 열은 **레코드 집합** 하위 요소에는 자체 하위 요소 또는 특성 (또는 둘 다) 이거나 하위의 부모에서 자식으로 하위 요소의 인스턴스가 둘 이상의 열입니다. 그렇지 않은 경우 열은 간단 합니다.

-   해당 열이 여러 개 (아래에서 다른 부모) 하위의 경우는 **Recordset** 열 경우 *모든* 인스턴스의 의미를 **레코드 집합** 열 해당 열이 간단한 경우에만 *모든* 인스턴스 단순 열을 의미 합니다.

-   모든 **레코드 집합** $Text 라는 추가 열을 포함 합니다.

 생성 하는 데 필요한 코드를 **레코드 집합** 는 다음과 같습니다.

```vb
Dim adoConn as ADODB.Connection
Dim adoRS as ADODB.Recordset

Set adoRS = New ADODB.Connection
Set adoRS = New ADODB.Recordset

adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
adoRS.Open "https://WebServer/VRoot/portfolio.xml, adoConn
```

> [!NOTE]
>  네 개의 다른 명명 규칙을 사용 하 여 데이터 파일의 경로 지정할 수 있습니다.

```vb
'HTTP://
adoRS.Open "https://WebServer/VRoot/portfolio.xml", adoConn
'FILE://
adoRS.Open "file:/// C:\\Directory\\portfolio.xml", adoConn
'UNC Path
adoRS.Open "\\ComputerName\ShareName\portfolio.xml", adoConn
'Full DOS Path
adoRS.Open "C:\Directory\portfolio.xml", adoConn
```

 즉시 합니다 **Recordset** 열린 일반적인 ADO **레코드 집합** 탐색 명령을 사용할 수 있습니다.

 **레코드 집합** 는 OSP에서 생성 된 몇 가지 제한 사항이 있습니다.

-   클라이언트 커서 (**adUseClient**) 지원 되지 않습니다.

-   계층적 **레코드 집합** 임의 통해 만든 XML 유지 될 수 없습니다를 사용 하 여 **Recordset.Save**합니다.

-   **레코드 집합** 는 OSP를 사용 하 여 만든 읽기 전용입니다.

-   각 데이터 ($Text)의 추가 열을 추가 하는 XMLDSO **레코드 집합** 계층 구조에서.

 OLE DB 단순 공급자에 대 한 자세한 내용은 참조 하세요. [단순 공급자 빌드](https://msdn.microsoft.com/b31a6cba-58ae-4ee8-9039-700973d354d6)합니다.

## <a name="code-example"></a>코드 예
 다음 Visual Basic 코드 계층을 생성, 임의의 XML 파일을 열면 하는 방법을 보여 줍니다 **Recordset**, 및 각각의 각 레코드를 작성 하는 재귀적으로 **레코드 집합** 디버그 창으로 합니다.

 주식 시세를 포함 하는 간단한 XML 파일을 다음과 같습니다. 다음 코드에서이 파일을 사용 하 여 두 수준의 계층을 생성 하 **레코드 집합**합니다.

```xml
<portfolio>
   <stock>
      <shares>100</shares>
      <symbol>MSFT</symbol>
      <price>$70.00</price>
      <info>
         <companyname>Microsoft Corporation</companyname>
         <website>https://www.microsoft.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>AAPL</symbol>
      <price>$107.00</price>
      <info>
         <companyname>Apple Computer, Inc.</companyname>
         <website>https://www.apple.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>DELL</symbol>
      <price>$50.00</price>
      <info>
         <companyname>Dell Corporation</companyname>
         <website>https://www.dell.com</website>
      </info>
    </stock>
    <stock>
       <shares>100</shares>
       <symbol>INTC</symbol>
       <price>$115.00</price>
       <info>
          <companyname>Intel Corporation</companyname>
          <website>https://www.intel.com</website>
       </info>
   </stock>
</portfolio>
```

 다음은 Visual Basic sub 프로시저입니다. 첫 번째 만듭니다는 **레코드 집합** 에 전달 합니다 *WalkHier* sub 프로시저를 재귀적으로 하위 계층에서 각 쓰기에서는 **필드** 각각의 각 레코드에서 **레코드 집합** 디버그 창에 있습니다.

```vb
Private Sub BrowseHierRecordset()
' Add ADO 2.7 or later to Project/References
' No need to add MSXML2, ADO just passes the ProgID through to the OSP.

    Dim adoConn As ADODB.Connection
    Dim adoRS As ADODB.Recordset
    Dim adoChildRS As ADODB.Recordset

    Set adoConn = New ADODB.Connection
    Set adoRS = New ADODB.Recordset
    Set adoChildRS = ADODB.Recordset

    adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
    adoRS.Open "https://bwillett3/Kowalski/portfolio.xml", adoConn

    Dim iLevel As Integer
    iLevel = 0
    WalkHier iLevel, adoRS

End Sub

Sub WalkHier(ByVal iLevel As Integer, ByVal adoRS As ADODB.Recordset)
    iLevel = iLevel + 1
    PriorLevel = iLevel
    While Not adoRS.EOF
        For ndx = 0 To adoRS.Fields.Count - 1
            If adoRS.Fields(ndx).Name <> "$Text" Then
                If adoRS.Fields(ndx).Type = adChapter Then
                    Set adoChildRS = adoRS.Fields(ndx).Value
                    WalkHier iLevel, adoChildRS
                Else
                    Debug.Print iLevel & ": adoRS.Fields(" & ndx & _
                       ") = " & adoRS.Fields(ndx).Name & " = " & _
                       adoRS.Fields(ndx).Value
                End If
            End If
        Next ndx
        adoRS.MoveNext
    Wend
    iLevel = PriorLevel
End Sub
```
