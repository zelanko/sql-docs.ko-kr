---
description: Microsoft OLE DB 단순 공급자 개요
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 81d60f33e0e9e055e086d990a681efb74cc943cc
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806529"
---
# <a name="microsoft-ole-db-simple-provider-overview"></a>Microsoft OLE DB 단순 공급자 개요
Microsoft OSP (OLE DB Simple Provider)를 사용 하면 ADO에서 [osp (OLE DB Simple provider) 도구 키트](/previous-versions/windows/desktop/ms715822(v=vs.85))를 사용 하 여 공급자가 작성 된 모든 데이터에 액세스할 수 있습니다. 단순 공급자는 메모리 내 배열 또는 XML 문서와 같이 기본적인 OLE DB 지원만 필요한 데이터 원본에 액세스 하기 위한 것입니다.

## <a name="connection-string-parameters"></a>연결 문자열 매개 변수
 OLE DB 단순 공급자 DLL에 연결 하려면 *provider* 인수를 [ConnectionString](../../reference/ado-api/connectionstring-property-ado.md) 속성으로 설정 합니다.

```vb
MSDAOSP
```

 이 값은 [공급자](../../reference/ado-api/provider-property-ado.md) 속성을 사용 하 여 설정 하거나 읽을 수도 있습니다.

 공급자 작성자가 결정 한 등록 된 공급자 이름을 사용 하 여 전체 OLE DB 공급자로 등록 된 단순 공급자에 연결할 수 있습니다.

## <a name="typical-connection-string"></a>일반 연결 문자열
 이 공급자에 대 한 일반적인 연결 문자열은 다음과 같습니다.

```vb
"Provider=MSDAOSP;Data Source=serverName"
```

 문자열은 다음과 같은 키워드로 구성 됩니다.

|키워드|설명|
|-------------|-----------------|
|**공급 기업**|SQL Server에 대 한 OLE DB 공급자를 지정 합니다.|
|**데이터 원본**|서버의 이름을 지정합니다.|

## <a name="xml-document-example"></a>XML 문서 예제
 MDAC 2.7 이상 및 windows DAC (Windows Data Access Components)의 OLE DB 단순 공급자 (OSP)는 임의의 XML 파일에 대 한 계층적 ADO **레코드 집합** 열기를 지원 하도록 향상 되었습니다. 이러한 XML 파일에는 ADO XML 지 속성 스키마가 포함 될 수 있지만 반드시 필요한 것은 아닙니다. 이는 **MSXML2.DLL**에 OSP를 연결 하 여 구현 되었습니다. 따라서 **MSXML2.DLL** 이상이 필요 합니다.

 다음 예제에 사용 된 **portfolio.xml** 파일에는 다음 트리가 포함 되어 있습니다.

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

 XML DSO는 기본 제공 추론을 사용 하 여 XML 트리의 노드를 계층적 **레코드 집합**의 장으로 변환 합니다.

 이러한 기본 제공 추론을 사용 하 여 XML 트리는 다음 형식의 두 수준 계층적 **레코드 집합** 으로 변환 됩니다.

```console
Parent Recordset
Shares, Symbol, Price, $Text
   Child Recordset
      Company Name, WebSite, $Text
```

 포트폴리오 및 정보 태그는 계층적 **레코드 집합**에 표시 되지 않습니다. XML DSO에서 XML 트리를 계층적 **레코드 집합**으로 변환 하는 방법에 대 한 설명은 다음 규칙을 참조 하세요. $Text 열에 대해서는 다음 섹션에서 설명 합니다.

## <a name="rules-for-assigning-xml-elements-and-attributes-to-columns-and-rows"></a>XML 요소 및 특성을 열 및 행에 할당 하는 규칙
 XML DSO는 데이터 바인딩된 응용 프로그램의 열 및 행에 요소와 특성을 할당 하는 절차를 따릅니다. XML은 전체 계층 구조를 포함 하는 하나의 태그를 사용 하는 트리로 모델링 됩니다. 예를 들어, 책에 대 한 XML 설명은 장 태그, 그림 태그 및 섹션 태그를 포함할 수 있습니다. 가장 높은 수준은 하위 요소 챕터, 그림 및 섹션을 포함 하는 책 태그입니다. XML DSO가 XML 요소를 행과 열에 매핑할 때 최상위 요소가 아닌 하위 요소가 변환 됩니다.

 XML DSO는 하위 요소를 변환 하는 데이 절차를 사용 합니다.

-   각 하위 요소와 특성은 계층의 일부 **레코드 집합** 에 있는 열에 해당 합니다.

-   부모 요소에 특성이 있고 이름이 같은 하위 요소가 없는 경우 열 이름은 하위 요소 또는 특성의 이름과 동일 합니다 .이 경우 "!"가 하위 요소의 열 이름 앞에와 야 합니다.

-   각 열은 스칼라 값 (일반적으로 문자열) 또는 자식 **레코드**집합을 포함 하는 **레코드 집합** 열을 포함 하는 *간단한* 열입니다.

-   특성에 해당 하는 열은 항상 단순 합니다.

-   하위 요소에 고유한 하위 요소나 특성 (또는 둘 다)이 있거나 하위 요소의 부모에 자식 요소인 하위 요소의 인스턴스가 두 개 이상 있는 경우 하위 요소에 해당 하는 열은 **레코드 집합** 열입니다. 그렇지 않으면 열이 단순 합니다.

-   하위 요소의 인스턴스가 여러 개 있는 경우 (다른 부모에 있는 경우) 해당 열이 **레코드 집합** 열을 의미 하 *는 경우 해당* 열은 **레코드 집합** 열입니다. *모든* 인스턴스가 단순 열을 의미 하는 경우에만 해당 열이 단순 합니다.

-   모든 **레코드 집합** 에는 $Text 이라는 추가 열이 있습니다.

 **레코드 집합** 을 생성 하는 데 필요한 코드는 다음과 같습니다.

```vb
Dim adoConn as ADODB.Connection
Dim adoRS as ADODB.Recordset

Set adoRS = New ADODB.Connection
Set adoRS = New ADODB.Recordset

adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
adoRS.Open "https://WebServer/VRoot/portfolio.xml, adoConn
```

> [!NOTE]
>  데이터 파일의 경로는 네 가지 명명 규칙을 사용 하 여 지정할 수 있습니다.

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

 **레코드 집합이** 열려 있는 즉시 일반적인 ADO **레코드 집합** 탐색 명령을 사용할 수 있습니다.

 OSP에 의해 생성 된 **레코드 집합** 에는 몇 가지 제한 사항이 있습니다.

-   클라이언트 커서 (**adUseClient**)는 지원 되지 않습니다.

-   임의 XML에 대해 만들어진 계층적 **레코드 집합** 은 **레코드 집합을**사용 하 여 유지할 수 없습니다. 저장.

-   OSP로 만든 **레코드 집합** 은 읽기 전용입니다.

-   XMLDSO는 계층의 각 **레코드 집합** 에 추가 데이터 열 ($Text)을 추가 합니다.

 OLE DB 단순 공급자에 대 한 자세한 내용은 [단순 공급자 빌드](/previous-versions/windows/desktop/ms721067(v=vs.85))를 참조 하세요.

## <a name="code-example"></a>코드 예
 다음 Visual Basic 코드는 임의의 XML 파일을 열고 계층적 **레코드 집합**을 생성 하 고 각 레코드 **집합** 의 각 레코드를 디버그 창에 재귀적으로 작성 하는 방법을 보여 줍니다.

 다음은 주식 시세를 포함 하는 간단한 XML 파일입니다. 다음 코드는이 파일을 사용 하 여 2 단계 계층적 **레코드 집합**을 생성 합니다.

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

 다음은 두 개의 Visual Basic 하위 프로시저입니다. 첫 번째는 **레코드 집합** 을 만들고 *WalkHier* sub 프로시저에 전달 합니다 .이 프로시저는 계층 구조를 재귀적으로 탐색 하 여 각 레코드 **집합** 의 각 레코드에 있는 각 **필드** 를 디버그 창에 기록 합니다.

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