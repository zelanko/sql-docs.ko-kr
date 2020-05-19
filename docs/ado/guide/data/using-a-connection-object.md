---
title: Connection 개체 사용 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
ms.assetid: 4b34f971-5699-43e7-9b15-137d334fa66e
author: rothja
ms.author: jroth
ms.openlocfilehash: ba23a9584e94df817e55b710ddadb073313e865b
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82750201"
---
# <a name="using-a-connection-object"></a>연결 개체 사용
**연결** 개체를 열기 전에 데이터 원본 및 연결 유형에 대 한 특정 정보를 정의 해야 합니다. 이러한 정보의 대부분은 **connection** 개체에서 [Open 메서드의](../../../ado/reference/ado-api/open-method-ado-connection.md) *connectionstring* 매개 변수 또는 **connection** 개체의 [connectionstring 속성](../../../ado/reference/ado-api/connectionstring-property-ado.md) 에 의해 유지 됩니다. 연결 문자열은 세미콜론으로 구분 된 인수/값 쌍의 목록으로 구성 됩니다. 값은 작은따옴표로 묶여 있습니다. 다음은 그 예입니다.  
  
```  
Dim sConn As String  
sConn = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Initial Catalog='Northwind';Integrated Security='SSPI';"  
```  
  
> [!NOTE]
>  ODBC DSN (데이터 원본 이름) 또는 연결 문자열에 있는 데이터 연결 (UDL) 파일을 지정할 수도 있습니다. Dsn에 대 한 자세한 내용은 ODBC 프로그래머 참조에서 [데이터 원본 관리](../../../odbc/admin/managing-data-sources.md) 를 참조 하십시오. Udl에 대 한 자세한 내용은 OLE DB 프로그래머 참조에서 [데이터 연결 API 개요](https://msdn.microsoft.com/95c180ea-bd4f-4dca-b95a-576afd135bbc) 를 참조 하세요.  
  
 일반적으로 적절 한 연결 *문자열* 을 매개 변수로 사용 하 여 **connection. Open** 메서드를 호출 하 여 연결을 설정 합니다. 다음 Visual Basic 코드 조각에 예제가 나와 있습니다.  
  
```  
Dim oConn As ADODB.Connection  
Dim oRs As ADODB.Recordset  
Dim sConn As String  
Dim sSQL as String  
  
' Open a connection.  
Set oConn = New ADODB.Connection  
.Open   
  
' Make a query over the connection.  
sSQL = "SELECT ProductID, ProductName, CategoryID, UnitPrice " & _  
             "FROM Products"  
Set oRs = New ADODB.Recordset  
oRs.Open sSQL, , adOpenStatic, adLockBatchOptimistic, adCmdText  
  
MsgBox oRs.RecordCount  
  
' Close the connection.  
oConn.Close  
Set oConn = Nothing  
  
```  
  
 여기서 **oRs** 는*Oconn*( **Connection** object) 변수를 해당 *ActiveConnection* 매개 변수의 값으로 사용 합니다. 또한 **CursorLocation** 속성은 **aduseserver**의 기본값을 가정 합니다. 이를 이전 섹션의 [HelloData](../../../ado/guide/data/hellodata-a-simple-ado-application.md) 예제와 대조 합니다. 다음 명령을 실행 하면 런타임 오류가 발생 합니다.  
  
```  
oRs.MarshalOptions = adMarshalModifiedOnly  
' Disconnect the Recordset.  
Set oRs.ActiveConnection = Nothing  
```
