---
title: 데이터 모양 지정 Visual Basic 예 | Microsoft Docs
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
dev_langs:
- VB
helpviewer_keywords:
- Visual Basic example of data shaping[ADO], about data shaping
ms.assetid: d95dd499-19e2-4ce7-b16e-f56a04a9519c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ee2240c6e44cc2d2ab3b63c5e060b70051a09568
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="visual-basic-example-of-data-shaping"></a>Visual Basic 예제에서는 데이터 모양 지정
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
  
#### <a name="try-it"></a>사용해 보세요!  
  
1.  표준 EXE Visual Basic 응용 프로그램 프로젝트 만들기  
  
2.  선택 **구성 요소** 에서 **프로젝트** Visual Studio에서 메뉴  
  
3.  "Microsoft 계층적 FlexGrid 제어 6.0 (OLEDB)"를 선택는 **구성 요소** 팝업 창 및 클릭 **저장**합니다.  
  
4.  Visual Basic 작업 영역에서 도구 상자 창에서 FlexGrid 컨트롤을 두 번 클릭 합니다. 이 인스턴스의 이름을 MSHFLEXGRID로 변경 합니다.  
  
5.  앞의 코드를 복사 하 고 붙여넣습니다는 **코드** 기존 코드를 바꿀 페이지입니다.  
  
6.  선택 **시작** 에서 **실행** 메뉴를 응용 프로그램을 실행 합니다.
