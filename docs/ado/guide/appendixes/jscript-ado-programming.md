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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7b9fe403c0d51d53e79d978ff573556b73f5aec7
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760499"
---
# <a name="jscript-ado-programming"></a>JScript ADO 프로그래밍
## <a name="creating-an-ado-project"></a>ADO 프로젝트 만들기  
 Microsoft JScript는 형식 라이브러리를 지원 하지 않으므로 프로젝트에서 ADO를 참조할 필요가 없습니다. 따라서 명령줄 완성 등의 관련 기능은 지원 되지 않습니다. 또한 기본적으로 ADO 열거 상수는 JScript에서 정의 되지 않습니다.  
  
 그러나 ADO는 JScript에서 사용할 다음 정의를 포함 하는 두 개의 포함 파일을 제공 합니다.  
  
-   서버 쪽 스크립팅에 대해 Adojavas를 사용 하 여 ADO 라이브러리 폴더에 설치 합니다.  
  
-   클라이언트 쪽 스크립팅에 대해 Adcjavas를 사용 하 여 ADO 라이브러리 폴더에 설치 합니다.  
  
 이러한 파일의 상수 정의를 복사 하 여 ASP 페이지에 붙여넣거나, 서버 쪽 스크립팅을 수행 하는 경우 Adojavas 파일을 웹 사이트의 폴더에 복사 하 고 다음과 같이 ASP 페이지에서 참조 합니다.  
  
```javascript
<!--#include File="adojavas.inc"-->  
```  
  
## <a name="creating-ado-objects-in-jscript"></a>JScript에서 ADO 개체 만들기  
 대신 **CreateObject** 함수 호출을 사용 해야 합니다.  
  
```javascript
var Rs1;  
Rs1 = Server.CreateObject("ADODB.Recordset");  
```  
  
## <a name="jscript-example"></a>JScript 예제  
 다음 코드는 **레코드 집합** 개체를 여는 Active Server 페이지 (ASP) 파일의 JScript 서버 쪽 프로그래밍에 대 한 일반적인 예입니다.  
  
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
