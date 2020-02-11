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
ms.openlocfilehash: 5a21eda26bab7f5bc5d678c6763c803323ffcff8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923502"
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
  
#### <a name="try-it"></a>시도해 보세요.  
  
1.  Visual Basic Standard EXE 응용 프로그램 프로젝트 만들기  
  
2.  Visual Studio의 **프로젝트** 메뉴에서 **구성 요소** 선택  
  
3.  **구성 요소** 팝업 창에서 "Microsoft 계층적 FlexGrid 컨트롤 6.0 (OLEDB)"을 선택 하 고 **저장**을 클릭 합니다.  
  
4.  Visual Basic 작업 영역의 도구 상자 창에서 FlexGrid 컨트롤을 두 번 클릭 합니다. 이 인스턴스의 이름을 MSHFLEXGRID로 변경 합니다.  
  
5.  위의 코드를 복사 하 여 **코드** 페이지에 붙여넣어 기존 코드를 바꿉니다.  
  
6.  응용 프로그램을 실행 하려면 **실행** 메뉴에서 **시작** 을 선택 합니다.
