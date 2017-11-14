---
title: "VBScript ADO 프로그래밍 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- ADO, VBScript
- VBScript [ADO]
ms.assetid: 6aaaf6d0-1376-4473-bea6-b81f2645a9ac
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bc40ecab95aa419ac81ada509133de6dd108a823
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="vbscript-ado-programming"></a>VBScript ADO 프로그래밍
## <a name="creating-an-ado-project"></a>ADO 프로젝트 만들기  
 Scripting Edition, Microsoft Visual Basic 프로젝트에서 ADO를 참조할 필요가 없습니다 있으므로 형식 라이브러리 지원 하지 않습니다. 따라서 연결된 기능은 명령줄 완료 같은 지원 되지 않습니다. 또한 기본적으로 열거 하는 ADO 상수 VBScript에서 정의 되지 않습니다.  
  
 그러나 ADO 제공 두 명의 VBScript 함께 사용 되는 다음 정의가 포함 된 파일을 포함 합니다.  
  
-   서버 쪽 스크립트 사용 Adovbs.inc 기본적으로 c:\Program Files\Common Files\System\ado\ 폴더에 설치 됩니다입니다.  
  
-   클라이언트 쪽 스크립트 사용 Adcvbs.inc 기본적으로 c:\Program Files\Common Files\System\msdac\ 폴더에 설치 됩니다입니다.  
  
 복사 및 이러한 파일에서 상수 정의에서는 ASP 페이지에 붙여 하거나, 서버 쪽 스크립팅 하는 경우 Adovbs.inc 파일을 웹 사이트의 폴더에 복사 하 고 다음과 같이 ASP 페이지에서 참조:  
  
```  
<!--#include File="adovbs.inc"-->  
```  
  
## <a name="creating-ado-objects-in-vbscript"></a>VBScript의 ADO 개체 만들기  
 사용할 수 없습니다는 **Dim** 문을 VBScript의 구체적인 형식으로 개체를 할당할 수 있습니다. VBScript를 지원 하지 않습니다는 **새로** 사용 되는 구문에서 **Dim** 응용 프로그램에 대 한 Visual Basic의 문입니다. 대신 사용 해야 합니다는 **CreateObject** 함수 호출:  
  
```  
Dim Rs1  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
```  
  
## <a name="vbscript-examples"></a>VBScript 예제  
 다음 코드는 Active Server 페이지 (ASP) 파일에서 VBScript 서버 쪽 프로그래밍의 일반적인 예:  
  
```  
<%  @LANGUAGE="VBSCRIPT" %>  
<%  Option Explicit %>  
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
  
 더 구체적인 VBScript 예 ADO 설명서에 포함 됩니다. 자세한 내용은 참조 [Microsoft Visual Basic Scripting Edition의 코드 예제 ADO](../../../ado/reference/ado-api/ado-code-examples-vbscript.md)합니다.  
  
## <a name="differences-between-vbscript-and-visual-basic"></a>VBScript와 Visual Basic의 차이점  
 VBScript와 함께 ADO 사용 구문이 사용 되는 방법을 비롯 한 다양 한 방식 Visual Basic을 사용한 ADO를 사용 하는 것과 비슷합니다. 그러나 몇 가지 중요 한 차이점이 존재 합니다.  
  
-   VBScript는 Variant 데이터 형식만 서로 다른 유형의 데이터를 저장할 수 있는 지원 합니다. Variant 데이터 형식에 필요한 데이터를 저장할 수 있습니다 및 데이터는 VBScript 수행한 캐스팅으로 인해 적절 하 게 작동 합니다. ADO에 필요한 형식을 인식 하 고 적절 하 게 변형에서 값으로 변환 합니다.  
  
-   사용할 수 없는 **오류 goto에 \<레이블 >** VBScript 내에서.  
  
-   VBScript와 같은 기본 제공 Visual Basic 함수 중 일부를 지원 **Msgbox**, **날짜**, 및 **IsNumeric**합니다. 그러나 VBScript Visual Basic의 하위 집합 이기 때문에 일부 기본 제공 함수는 지원 됩니다. 예를 들어 VBScript 지원 하지 않습니다는 **형식** 파일 I/O 함수입니다.

