---
title: VBScript ADO 프로그래밍 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a9c13b532e1ac234c207fc70fe7578be341f72b4
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701130"
---
# <a name="vbscript-ado-programming"></a>VBScript ADO 프로그래밍
## <a name="creating-an-ado-project"></a>ADO 프로젝트 만들기  
 Microsoft Visual Basic, Scripting Edition 지원 하지 않으므로 형식 라이브러리 프로젝트에서 ADO를 참조할 필요가 없습니다. 따라서 명령줄 완성과 같은 관련된 없는 기능 지원 됩니다. 또한 기본적으로 ADO 열거 상수 VBScript에서 정의 되지 않습니다.  
  
 그러나 ADO 제공 두 명의 VBScript와 함께 사용 될 다음 정의 포함 하는 파일을 포함 합니다.  
  
-   서버 쪽 스크립팅 사용 Adovbs.inc 기본적으로는 c:\Program Files\Common Files\System\ado\ 폴더에 설치 됩니다.  
  
-   클라이언트 쪽 스크립팅 사용 Adcvbs.inc 기본적으로는 c:\Program Files\Common Files\System\msdac\ 폴더에 설치 됩니다.  
  
 복사 및 ASP 페이지에 이러한 파일에서 상수 정의 붙여 하거나, 서버 쪽 스크립팅, 수행 하는 경우 웹 사이트의 폴더로 Adovbs.inc 파일을 복사 하 고 다음과 같은 ASP 페이지에서 참조 합니다.  
  
```vb
<!--#include File="adovbs.inc"-->  
```  
  
## <a name="creating-ado-objects-in-vbscript"></a>Vbscript에서 ADO 개체 만들기  
 사용할 수 없습니다는 **Dim** VBScript의 특정 형식으로 개체를 할당 하는 문입니다. 또한 VBScript을 지원 하지 않습니다는 **새로 만들기** 구문을 사용 합니다 **Dim** 응용 프로그램에 대 한 Visual Basic의 문입니다. 대신 사용 해야 합니다 **CreateObject** 함수 호출:  
  
```vb
Dim Rs1  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
```  
  
## <a name="vbscript-examples"></a>VBScript 예제  
 다음 코드는 페이지 ASP (Active Server) 파일에서 VBScript 서버 쪽 프로그래밍의 일반적인 예:  
  
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
  
 보다 구체적인 VBScript 예제 ADO 설명서에 포함 됩니다. 자세한 내용은 [Microsoft Visual Basic Scripting Edition의 ADO 코드 예제](../../../ado/reference/ado-api/ado-code-examples-vbscript.md)합니다.  
  
## <a name="differences-between-vbscript-and-visual-basic"></a>VBScript 및 Visual Basic 간의 차이점  
 Vbscript ADO를 사용 하 여 Visual Basic을 사용 하 여 ADO를 사용 하 여 구문을 사용 하는 방법을 비롯 한 다양 한 방식에 것과 비슷합니다. 그러나 중요 한 차이점이 몇 개 있습니다.  
  
-   VBScript만 Variant 데이터 형식의 다양 한 유형의 데이터를 저장할 수 있는 지원 합니다. Variant 데이터 형식에 필요한 데이터를 저장할 수 있습니다 및 VBScript 수행한 캐스팅으로 인해 데이터를 적절 하 게 작동 합니다. ADO에 필요한 형식을 인식 하 고 적절 하 게 변형 값으로 변환 합니다.  
  
-   사용할 수 없습니다 **에서 오류 goto \<레이블 >** VBScript 내에서.  
  
-   VBScript와 같은 기본 제공 Visual Basic 함수 중 일부를 지원 **Msgbox**하십시오 **날짜**, 및 **IsNumeric**합니다. 그러나 VBScript Visual Basic의 하위 집합 이기 때문에 일부 기본 제공 함수는 지원 됩니다. 예를 들어, VBScript 지원 하지 않습니다 합니다 **형식** 함수와 파일 I/O 함수입니다.
