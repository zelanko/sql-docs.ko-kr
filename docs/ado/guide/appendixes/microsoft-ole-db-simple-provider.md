---
title: "간단한 Microsoft OLE DB Provider | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- simple provider [ADO]
- providers [ADO], OLE DB simple provider
- OLE DB simple provider [ADO]
ms.assetid: 1e7dc6f0-482c-4103-8187-f890865e40fc
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b81dae92dcb8f6493fd6d6c74515750d4e4a0f66
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-ole-db-simple-provider-overview"></a>Microsoft OLE DB 공급자 간단한 개요
Microsoft OLE DB 간단한 공급자 (OSP)는에 대 한 공급자를 썼는지를 사용 하 여 데이터에 액세스할 수는 ADO를 사용 하면는 [OLE DB 간단한 공급자 (OSP) Toolkit](http://msdn.microsoft.com/en-us/6e7b7931-9e4a-4151-ae51-672abd3f84a6)합니다. 간단한 공급자는 메모리 내 배열 또는 XML 문서와 같은 기본만 OLE DB 지원 해야 하는 데이터 원본에 액세스 하는 데 사용 됩니다.

## <a name="connection-string-parameters"></a>연결 문자열 매개 변수
 OLE DB 간단한 공급자 DLL에 연결할 설정는 *공급자* 인수에는 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성을:

```
MSDAOSP
```

 이 값도 설정 하거나 사용 하 여 읽을 수는 [공급자](../../../ado/reference/ado-api/provider-property-ado.md) 속성입니다.

 공급자 기록기에 의해 결정 된 등록 된 공급자 이름을 사용 하 여 전체 OLE DB 공급자로 등록 된 간단한 공급자에 연결할 수 있습니다.

## <a name="typical-connection-string"></a>일반적인 연결 문자열
 이 공급자에 대 한 일반적인 연결 문자열은:

```
"Provider=MSDAOSP;Data Source=serverName"
```

 이러한 키워드의 문자열 구성 됩니다.

|키워드|Description|
|-------------|-----------------|
|**공급자**|SQL Server 용 OLE DB 공급자를 지정합니다.|
|**데이터 원본**|서버 이름을 지정합니다.|

## <a name="xml-document-example"></a>XML 문서 예제
 OLE DB 간단한 공급자 (OSP) MDAC 2.7 이상 및 Windows Data Access Components (Windows DAC) 계층적 ADO 열기를 지원 하도록 향상 되었습니다 **레코드 집합** 임의의 XML 파일에 비해 합니다. 이러한 XML 파일에는 ADO XML 지 속성 스키마를 포함 될 수 있지만 필요 하지 않습니다. OSP를 연결 하 여 구현 되었습니다이 **MSXML2.DLL**; 따라서 **MSXML2.DLL** 이상 버전이 필요 합니다.

 **portfolio.xml** 다음 트리를 포함 하는 다음 예제에서 사용 되는 파일:

```
Portfolio
   Stock
      Shares
      Symbol
      Price
      Info
         Company Name
         WebSite
```

 XML DSO에서 기본 제공 휴리스틱을 사용 하 여 XML 트리의 노드는 계층적 장 변환할 **레코드 집합**합니다.

 이러한 기본 제공 추론을 사용 하 여 XML 트리는 두 수준의 계층으로 변환 됩니다 **레코드 집합** 다음과 같은 형식의:

```
Parent Recordset
Shares, Symbol, Price, $Text
   Child Recordset
      Company Name, WebSite, $Text
```

 포트폴리오 및 정보 태그는 계층적 표현 되지 않는 참고 **레코드 집합**합니다. XML DSO 계층적에 XML 트리를 변환 하는 방법에 대 한 설명은 **레코드 집합**, 다음 규칙을 참조 하십시오. $Text 열 다음 섹션에서 설명 합니다.

## <a name="rules-for-assigning-xml-elements-and-attributes-to-columns-and-rows"></a>열과 행에 할당 XML 요소와 특성에 대 한 규칙
 XML DSO 요소를 할당 하기 위한 절차 다음에 나오는 및 데이터 바인딩된 응용 프로그램의 열과 행 특성 합니다. XML은 전체 계층 구조를 포함 하는 한 태그를 사용 하 여 트리도 모델링 됩니다. 예를 들어, 책에 대 한 XML 설명을 장 태그, 도형 태그 및 태그 섹션 포함 될 수 있습니다. 최상위 수준의 것 하위 요소가 장, 그림 및 섹션을 포함 하는 책 태그입니다. XML DSO를 행과 열으로 XML 요소를 맵, 최상위 수준 요소가 아닌 하위 요소가 변환 됩니다.

 이 절차를 사용 하 여 하위 요소를 변환 하기 위한 XML DSO:

-   일부의 열에 해당 하는 각 하위 요소와 특성 **레코드 집합** 계층 구조에서.

-   열의 이름이 되지 않으면 오류가 하위 요소 또는 특성의 이름과 동일한 경우 부모 요소에는 특성과 동일한 이름 가진 하위 요소는 "!" 앞 subelement의 열 이름에 추가 됩니다.

-   각 열은 하나는 *간단한* 스칼라 값 (일반적으로 문자열)이 포함 된 열 또는 **레코드 집합** 자식 포함 된 열 **레코드 집합**합니다.

-   특성에 해당 하는 열은 항상 단순 합니다.

-   하위 요소에 해당 하는 열은 **레코드 집합** 하위는 자체 하위 요소 또는 특성 (또는 둘 다) 나 된 하위 요소의 부모에 자식으로 하위 요소 둘 이상의 인스턴스가 하는 경우에 열입니다. 그렇지 않은 경우 열은 간단 합니다.

-   해당 열이 있는 경우 (서로 다른 부모)에서 하위 요소를 여러 개, 한 **레코드 집합** 열 경우 *모든* 인스턴스의 의미는 **레코드 집합** 열; 해당 열이 단순한 경우에만 *모든* 인스턴스 단순 열을 의미 합니다.

-   모든 **레코드 집합** $Text 라는 추가 열이 있어야 합니다.

 생성 하는 데 필요한 코드는 **레코드 집합** 는 다음과 같습니다.

```
Dim adoConn as ADODB.Connection
Dim adoRS as ADODB.Recordset

Set adoRS = New ADODB.Connection
Set adoRS = New ADODB.Recordset

adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
adoRS.Open "http://WebServer/VRoot/portfolio.xml, adoConn
```

> [!NOTE]
>  네 개의 서로 다른 명명 규칙을 사용 하 여 데이터 파일의 경로 지정할 수 있습니다.

```
'HTTP://
adoRS.Open "http://WebServer/VRoot/portfolio.xml", adoConn
'FILE://
adoRS.Open "file:/// C:\\Directory\\portfolio.xml", adoConn
'UNC Path
adoRS.Open "\\ComputerName\ShareName\portfolio.xml", adoConn
'Full DOS Path
adoRS.Open "C:\Directory\portfolio.xml", adoConn
```

 즉시는 **레코드 집합** 열린 일반적인 ADO **레코드 집합** 탐색 명령도 사용할 수 있습니다.

 **레코드 집합** 는 OSP에 의해 생성 된 몇 가지 제한 사항이 있습니다.

-   클라이언트 커서 (**adUseClient**)는 지원 되지 않습니다.

-   계층적 **레코드 집합** 임의의에 만든 XML 유지할 수 없는 사용 하 여 **Recordset.Save**합니다.

-   **레코드 집합** 는 OSP를 사용 하 여 만든은 읽기 전용입니다.

-   각 데이터 ($Text)의 추가 열을 추가 하는 XMLDSO **레코드 집합** 계층 구조에서.

 OLE DB 간단한 공급자에 대 한 자세한 내용은 참조 [간단한 공급자 빌드](http://msdn.microsoft.com/en-us/b31a6cba-58ae-4ee8-9039-700973d354d6)합니다.

## <a name="code-example"></a>코드 예
 다음 Visual Basic 코드 생성을 계층적 구조는 임의의 XML 파일을 보여 줍니다. **레코드 집합**, 반복적으로 각각의 각 레코드를 쓰는 **레코드 집합** 디버그 창에 있습니다.

 다음은 주식 시세를 포함 하는 간단한 XML 파일입니다. 다음 코드에서이 파일을 사용 하 여 두 수준의 계층 구조를 생성 하 **레코드 집합**합니다.

```
<portfolio>
   <stock>
      <shares>100</shares>
      <symbol>MSFT</symbol>
      <price>$70.00</price>
      <info>
         <companyname>Microsoft Corporation</companyname>
         <website>http://www.microsoft.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>AAPL</symbol>
      <price>$107.00</price>
      <info>
         <companyname>Apple Computer, Inc.</companyname>
         <website>http://www.apple.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>DELL</symbol>
      <price>$50.00</price>
      <info>
         <companyname>Dell Corporation</companyname>
         <website>http://www.dell.com</website>
      </info>
    </stock>
    <stock>
       <shares>100</shares>
       <symbol>INTC</symbol>
       <price>$115.00</price>
       <info>
          <companyname>Intel Corporation</companyname>
          <website>http://www.intel.com</website>
       </info>
   </stock>
</portfolio>
```

 다음은 Visual Basic sub 프로시저입니다. 첫 번째 만듭니다는 **레코드 집합** 에 전달 된 *WalkHier* sub 프로시저를 작성 하는 각 계층 구조 아래로 재귀적으로 안내 **필드** 각각의 각 레코드에 **레코드 집합** 디버그 창에 있습니다.

```
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
    adoRS.Open "http://bwillett3/Kowalski/portfolio.xml", adoConn

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

