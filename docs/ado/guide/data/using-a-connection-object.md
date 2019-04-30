---
title: 연결 개체를 사용 하 여 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d7726cb0aeeade66870b1b3d175a9489a93bad09
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184958"
---
# <a name="using-a-connection-object"></a>연결 개체 사용
열기 전에 **연결** 개체를 데이터 원본 및 연결 형식에 대 한 특정 정보를 정의 해야 합니다. 대부분의이 정보에서 유지 되는 *ConnectionString* 의 매개 변수를 [Open 메서드](../../../ado/reference/ado-api/open-method-ado-connection.md) 에 **연결** 개체를 또는 [ConnectionString 속성](../../../ado/reference/ado-api/connectionstring-property-ado.md) 에 **연결** 개체입니다. 연결 문자열을 작은따옴표로 묶인 값과 세미콜론으로 구분 된 인수/값 쌍의 목록으로 구성 됩니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
Dim sConn As String  
sConn = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Initial Catalog='Northwind';Integrated Security='SSPI';"  
```  
  
> [!NOTE]
>  또한 연결 문자열에는 ODBC 데이터 원본 이름 (DSN) 또는 데이터 연결 (UDL) 파일을 지정할 수 있습니다. Dsn에 대 한 자세한 내용은 참조 하세요. [데이터 원본 관리](../../../odbc/admin/managing-data-sources.md) 의 ODBC 프로그래머 참조입니다. Udl에 대 한 자세한 내용은 참조 하세요. [데이터 링크 API 개요](https://msdn.microsoft.com/95c180ea-bd4f-4dca-b95a-576afd135bbc) OLE DB 프로그래머 참조에서입니다.  
  
 일반적으로 호출 하 여 연결을 설정한 합니다 **Connection.Open** 적절 한 메서드는 *연결 문자열* 매개 변수로 합니다. 예제는 다음 Visual Basic 코드 조각에 나와 있습니다.  
  
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
  
 여기 **oRs.Open** 사용을 **연결** 개체 (*oConn*) 값으로 변수 해당 *ActiveConnection* 매개 변수입니다. 또한 합니다 **Connection.CursorLocation** 속성의 기본값 가정 **가 adUseServer**합니다. 이를 대조해 보세요 합니다 [HelloData](../../../ado/guide/data/hellodata-a-simple-ado-application.md) 이전 섹션의 예제입니다. 다음 명령은 런타임 오류가 발생 합니다.  
  
```  
oRs.MarshalOptions = adMarshalModifiedOnly  
' Disconnect the Recordset.  
Set oRs.ActiveConnection = Nothing  
```
