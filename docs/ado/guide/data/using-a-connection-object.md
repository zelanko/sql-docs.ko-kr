---
title: 연결 개체를 사용 하 여 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
ms.assetid: 4b34f971-5699-43e7-9b15-137d334fa66e
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7aa8e57d79b7f65ede84c7e88f03d18a5131f449
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="using-a-connection-object"></a>연결 개체를 사용 하 여
열기 전에 **연결** 개체를 데이터 원본 및 연결의 종류에 대 한 정보를 정의 해야 합니다. 이 정보의 대부분 보유는 *ConnectionString* 의 매개 변수는 [Open 메서드](../../../ado/reference/ado-api/open-method-ado-connection.md) 에 **연결** 개체 또는 [ConnectionString 속성](../../../ado/reference/ado-api/connectionstring-property-ado.md) 에 **연결** 개체입니다. 연결 문자열을 작은따옴표 내에 포함 된 값을 가진 세미 콜론으로 구분 된 인수/값 쌍의 목록으로 구성 합니다. 예를 들어:  
  
```  
Dim sConn As String  
sConn = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Initial Catalog='Northwind';Integrated Security='SSPI';"  
```  
  
> [!NOTE]
>  또한 연결 문자열에는 ODBC 데이터 원본 이름 (DSN) 또는 데이터 링크 (UDL) 파일을 지정할 수 있습니다. Dsn에 대 한 자세한 내용은 참조 [데이터 원본 관리](../../../odbc/admin/managing-data-sources.md) ODBC 프로그래머 참조에서 합니다. Udl에 대 한 자세한 내용은 참조 [데이터 링크 API 개요](http://msdn.microsoft.com/en-us/95c180ea-bd4f-4dca-b95a-576afd135bbc) OLE DB 프로그래머 참조에서.  
  
 호출 하 여 연결을 설정 하는 일반적으로 **Connection.Open** 가능한 적절 한 메서드는 *연결 문자열* 매개 변수로 합니다. 예는 다음 Visual Basic 코드 조각에 표시 됩니다.  
  
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
  
 여기 **oRs.Open** 사용는 **연결** 개체 (*oConn*)의 값으로 변수 해당 *ActiveConnection* 매개 변수입니다. 또한는 **Connection.CursorLocation** 속성의 기본값을 가정 **가 adUseServer**합니다. 이와 반대로 하는 [HelloData](../../../ado/guide/data/hellodata-a-simple-ado-application.md) 이전 섹션의 예제. 다음 명령 실행 시 오류가 발생 합니다.  
  
```  
oRs.MarshalOptions = adMarshalModifiedOnly  
' Disconnect the Recordset.  
Set oRs.ActiveConnection = Nothing  
```
