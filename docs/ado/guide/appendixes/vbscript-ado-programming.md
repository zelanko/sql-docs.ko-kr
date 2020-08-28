---
description: VBScript ADO 프로그래밍
title: VBScript ADO 프로그래밍 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ADO, VBScript
- VBScript [ADO]
ms.assetid: 6aaaf6d0-1376-4473-bea6-b81f2645a9ac
author: rothja
ms.author: jroth
ms.openlocfilehash: 6b89d247f5bc91ca0b3494c15d3781116b8c9614
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990924"
---
# <a name="vbscript-ado-programming"></a>VBScript ADO 프로그래밍
## <a name="creating-an-ado-project"></a>ADO 프로젝트 만들기  
 Microsoft Visual Basic, Scripting Edition은 형식 라이브러리를 지원 하지 않으므로 프로젝트에서 ADO를 참조할 필요가 없습니다. 따라서 명령줄 완성 등의 관련 기능은 지원 되지 않습니다. 또한 기본적으로 ADO 열거 상수는 VBScript에서 정의 되지 않습니다.  
  
 그러나 ADO에서는 VBScript와 함께 사용할 다음 정의를 포함 하는 두 개의 포함 파일을 제공 합니다.  
  
-   서버 쪽 스크립팅에 Adovbs를 사용 합니다 .이는 기본적으로 c:\Program Files\Common Files\System\ado\ 폴더에 설치 됩니다.  
  
-   클라이언트 쪽 스크립팅에 대해 기본적으로 c:\Program Files\Common Files\System\msdac\ 폴더에 설치 되는 Adcvbs inc.를 사용 합니다.  
  
 이러한 파일의 상수 정의를 복사 하 여 ASP 페이지에 붙여넣거나, 서버 쪽 스크립팅을 수행 하는 경우 Adovbs 파일을 웹 사이트의 폴더에 복사 하 고 다음과 같이 ASP 페이지에서 참조 합니다.  
  
```vb
<!--#include File="adovbs.inc"-->  
```  
  
## <a name="creating-ado-objects-in-vbscript"></a>VBScript에서 ADO 개체 만들기  
 VBScript의 특정 형식에 개체를 할당 하는 데 **Dim** 문을 사용할 수 없습니다. 또한 VBScript는 Visual Basic for Applications에서 **Dim** 문에 사용 되는 **새** 구문을 지원 하지 않습니다. 대신 **CreateObject** 함수 호출을 사용 해야 합니다.  
  
```vb
Dim Rs1  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
```  
  
## <a name="vbscript-examples"></a>VBScript 예제  
 다음 코드는 ASP (Active Server 페이지) 파일에서 VBScript 서버 쪽 프로그래밍의 일반적인 예입니다.  
  
```vb
<%  @LANGUAGE="VBSCRIPT" %>  
<%  Option Explicit %>  
<!--#include File="adovbs.inc"-->  
<HTML>  
    <BODY BGCOLOR="White" topmargin="10" leftmargin="10">  
  
    <!-- Your ASP Code goes here -->  
<%  
Dim Source  
Dim Connect  
Dim Rs1  
  
Source = "SELECT * FROM Authors"  
Connect = "Provider=sqloledb;Data Source=srv;" & _  
    "Initial Catalog=Pubs;Integrated Security=SSPI;"  
  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
Rs1.Open Source, Connect, adOpenForwardOnly  
Response.Write("Success!")  
%>  
    </BODY>  
</HTML>  
```  
  
 보다 구체적인 VBScript 예제가 ADO 설명서에 포함 되어 있습니다. 자세한 내용은 [Microsoft Visual Basic Scripting Edition의 ADO 코드 예제](../../reference/ado-api/ado-code-examples-vbscript.md)를 참조 하세요.  
  
## <a name="differences-between-vbscript-and-visual-basic"></a>VBScript와 Visual Basic의 차이점  
 VBScript와 함께 ado를 사용 하는 것은 구문을 사용 하는 방법을 비롯 하 여 여러 가지 방법으로 Visual Basic ADO를 사용 하는 것과 비슷합니다 그러나 다음과 같은 몇 가지 중요 한 차이점이 있습니다.  
  
-   VBScript는 여러 유형의 데이터를 보유할 수 있는 Variant 데이터 형식만 지원 합니다. 필요한 데이터를 Variant 데이터 형식에 저장할 수 있으며 VBScript에서 수행 하는 캐스팅으로 인해 데이터가 제대로 작동 합니다. ADO에서 요구 하는 형식을 인식 하 고이에 따라 변형의 값을 변환 합니다.  
  
-   VBScript 내 **에서는 오류 발생 시 \<label> goto를** 사용할 수 없습니다.  
  
-   VBScript는 **Msgbox**, **Date**및 **IsNumeric**와 같은 일부 기본 제공 Visual Basic 기능을 지원 합니다. 그러나 VBScript는 Visual Basic의 하위 집합 이기 때문에 일부 기본 제공 함수는 지원 되지 않습니다. 예를 들어 VBScript는 **Format** 함수 및 파일 i/o 함수를 지원 하지 않습니다.