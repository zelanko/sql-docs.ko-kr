---
title: JScript ADO 프로그래밍 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- JScript
helpviewer_keywords:
- JScript programming in ADO
- ADO, JScript programming
ms.assetid: 62273658-0fe7-4aac-b4d8-f725e6baf043
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec620ba868a6a72af224b4fc17d0339936d8b48c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="jscript-ado-programming"></a>JScript ADO 프로그래밍
## <a name="creating-an-ado-project"></a>ADO 프로젝트 만들기  
 Microsoft JScript 불필요 ADO 참조를 프로젝트에 있으므로 형식 라이브러리를 지원 하지 않습니다. 따라서 연결된 기능은 명령줄 완료 같은 지원 되지 않습니다. 또한 기본적으로 열거 하는 ADO 상수 jscript에서 정의 되지 않습니다.  
  
 그러나 ADO 제공 두 명의 JScript에서 사용 되는 다음 정의가 포함 된 파일을 포함 합니다.  
  
-   서버 쪽 스크립트 사용 Adojavas.inc는 ADO 라이브러리 폴더에 설치 됩니다.  
  
-   클라이언트 쪽 스크립트 사용 Adcjavas.inc는 ADO 라이브러리 폴더에 설치 됩니다.  
  
 복사 하 고 이러한 파일에서 상수 정의에서는 ASP 페이지에 붙여 넣을 하거나, Adojavas.inc 파일을 웹 사이트의 폴더에 복사 하 고 다음과 같이 ASP 페이지에서 참조 하는 서버 쪽 스크립팅 하는 경우:  
  
```  
<!--#include File="adojavas.inc"-->  
```  
  
## <a name="creating-ado-objects-in-jscript"></a>Jscript에서 ADO 개체 만들기  
 대신 사용 해야 합니다는 **CreateObject** 함수 호출:  
  
```  
var Rs1;  
Rs1 = Server.CreateObject("ADODB.Recordset");  
```  
  
## <a name="jscript-example"></a>JScript 예제  
 다음 코드는 열리면 페이지 ASP (Active Server) 파일에 JScript 서버 쪽 프로그래밍의 일반적인 예는 **레코드 집합** 개체:  
  
```  
<%  @LANGUAGE="JScript" %>  
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
