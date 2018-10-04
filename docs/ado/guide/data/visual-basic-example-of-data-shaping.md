---
title: 데이터 셰이핑의 Visual Basic 예 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Visual Basic example of data shaping[ADO], about data shaping
ms.assetid: d95dd499-19e2-4ce7-b16e-f56a04a9519c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 772fb84482346402133874ff5e177f4d3c8b30c4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47645641"
---
# <a name="visual-basic-example-of-data-shaping"></a>데이터 셰이핑의 Visual Basic 예제
```  
' This application makes use of Microsoft Hierarchical FlexGrid  
' Control, which is named as MSHFLexGrid.  
Const SHAPER = "MSDataShape"  
Const DP = "SQLOLEDB"  
Const DS = "MySQLServer"  
Const DB = "Northwind"  
  
Private Sub Form_Load()  
    FirstExample  
End Sub  
  
Private Sub Form_Resize()  
    MSHFlexGrid.Top = 0  
    MSHFlexGrid.Left = 0  
    MSHFlexGrid.Width = Me.ScaleWidth  
    MSHFlexGrid.Height = Me.ScaleHeight  
End Sub  
  
Private Sub FirstExample()  
    Dim con As ADODB.Connection  
    Dim rst As ADODB.Recordset  
    Dim sCmd As String  
  
    Set con = New ADODB.Connection  
    Set rst = New ADODB.Recordset  
  
    con.ConnectionString = ConnectionString(SHAPER, DP, DS, DB)  
    con.Open  
  
    sCmd = "SHAPE {SELECT CustomerID, ContactName FROM Customers} " _  
        & "APPEND ({SELECT OrderID, OrderDate, CustomerID FROM Orders} " _  
        & "AS chapOrders " _  
        & "RELATE customerID TO customerID)"  
  
    rst.Open sCmd, con, adOpenStatic, 2  
    Set MSHFlexGrid.Recordset = rst  
  
    rst.Close  
    Set rst = Nothing  
  
    con.Close  
    Set con = Nothing  
  
End Sub  
  
Private Function ConnectionString(pr As String, _  
                                  dpr As String, _  
                                  dsr As String, _  
                                  dbs As String)  
    Dim s As String  
    If pr = "" Then  
        s = "Provider=" & dpr & _  
          ";Data Source=" & dsr & _  
          ";Initial Catalog=" & dbs & _  
          ";Integrated Security=SSPI;"  
    Else  
        s = "Provider=" & pr & _  
          ";Data Provider=" & dpr & _  
          ";Data Source=" & dsr & _  
          ";Initial Catalog=" & dbs & _  
          ";Integrated Security=SSPI;"  
    End If  
    ConnectionString = s  
End Function  
  
```  
  
#### <a name="try-it"></a>지금 사용해 보세요!  
  
1.  표준 EXE Visual Basic 응용 프로그램 프로젝트 만들기  
  
2.  선택 **구성 요소** 에서 합니다 **프로젝트** Visual Studio의 메뉴  
  
3.  "Microsoft 계층적 FlexGrid 컨트롤 6.0 (OLEDB)"를 선택 합니다 **구성 요소** 팝업 창과 클릭 **저장**합니다.  
  
4.  Visual Basic 작업 영역의 도구 상자 창에서 FlexGrid 컨트롤을 두 번 클릭 합니다. MSHFLEXGRID이 인스턴스의 이름을 변경 합니다.  
  
5.  앞의 코드를 복사 하 고 붙여 넣습니다 합니다 **코드** 기존 코드를 바꿀 페이지입니다.  
  
6.  선택 **시작** 에서 합니다 **실행** 메뉴는 응용 프로그램을 실행 합니다.
