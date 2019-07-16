---
title: JScript ADO 프로그래밍 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- JScript
helpviewer_keywords:
- JScript programming in ADO
- ADO, JScript programming
ms.assetid: 62273658-0fe7-4aac-b4d8-f725e6baf043
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8d07759405dc337667cc8971ce7795af428a0cfa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926809"
---
# <a name="jscript-ado-programming"></a>JScript ADO 프로그래밍
## <a name="creating-an-ado-project"></a>ADO 프로젝트 만들기  
 Microsoft JScript 있습니다 하지 않아도 되므로 ADO 참조 프로젝트에서 형식 라이브러리를 지원 하지 않습니다. 따라서 명령줄 완성과 같은 관련된 없는 기능 지원 됩니다. 또한 기본적으로 ADO 열거 상수 JScript에서 정의 되지 않습니다.  
  
 그러나 ADO 제공 두 명의 JScript를 사용 하 여 사용할 다음 정의 포함 하는 파일을 포함 합니다.  
  
-   서버 쪽 스크립팅 사용 Adojavas.inc는 ADO 라이브러리 폴더에 설치 됩니다.  
  
-   클라이언트 쪽 스크립트 사용 Adcjavas.inc는 ADO 라이브러리 폴더에 설치 됩니다.  
  
 복사 및 ASP 페이지에 이러한 파일에서 상수 정의 붙여 넣습니다. 하거나, 서버 쪽 스크립팅, 수행 하는 경우 웹 사이트의 폴더로 Adojavas.inc 파일을 복사 하 고 다음과 같은 ASP 페이지에서 참조 합니다.  
  
```javascript
<!--#include File="adojavas.inc"-->  
```  
  
## <a name="creating-ado-objects-in-jscript"></a>JScript의 ADO 개체 만들기  
 대신 사용 해야 합니다 **CreateObject** 함수 호출:  
  
```javascript
var Rs1;  
Rs1 = Server.CreateObject("ADODB.Recordset");  
```  
  
## <a name="jscript-example"></a>JScript 예제  
 다음 코드는 열리는 페이지 ASP (Active Server) 파일에서 JScript 서버 쪽 프로그래밍의 일반적인 예는 **레코드 집합** 개체:  
  
```javascript
<%  @LANGUAGE="JScript" %>  
<!--#include File="adojavas.inc"-->  
<HTML>  
<BODY BGCOLOR="White" topmargin="10" leftmargin="10">  
<%  
var Source = "SELECT * FROM Authors";  
var Connect =  "Provider=sqloledb;Data Source=srv;" +  
    "Initial Catalog=Pubs;Integrated Security=SSPI;"  
var Rs1 = Server.CreateObject( "ADODB.Recordset.2.5" );  
Rs1.Open(Source,Connect,adOpenForwardOnly);  
Response.Write("Success!");  
%>  
</BODY>  
</HTML>  
```
