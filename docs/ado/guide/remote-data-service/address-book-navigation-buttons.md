---
title: 주소록 탐색 단추 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS scenarios [ADO], navigation buttons
- address book application scenario [ADO], navigation buttons
ms.assetid: f0dd84c6-5c33-4ab9-82b4-4c42dfdd2277
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 60d3b2660f3a20883e9b9f2d3b4202526c15a943
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242791"
---
# <a name="address-book-navigation-buttons"></a>주소록 탐색 단추
주소록 응용 프로그램 웹 페이지의 맨 아래에 있는 탐색 단추를 표시합니다. 데이터의 첫 번째 또는 마지막 행 또는 현재 선택 영역에 인접 한 행 중 하나를 선택 하 여 HTML 눈금 표시의 데이터를 탐색할 수 있는 탐색 단추를 사용할 수 있습니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="navigation-sub-procedures"></a>탐색 Sub 프로시저  
 주소록 응용 프로그램에는 사용자가 클릭 하도록 허용 하는 몇 가지 절차가 포함 되어 있습니다.는 **첫 번째**를 **다음**합니다 **이전**, 및 **마지막** 데이터를 이동 하는 단추입니다.  
  
 예를 들어,를 클릭 하 여 **첫 번째** VBScript First_OnClick Sub 프로시저를 활성화 하는 단추입니다. 프로시저 실행을 [MoveFirst](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) 메서드를 현재 선택 영역에 데이터의 첫 번째 행으로 만듭니다. 클릭 하는 **마지막** 단추가 활성화 Last_OnClick Sub 프로시저를 호출 하는 합니다 [MoveLast](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) 메서드, 데이터의 마지막 행을 현재 선택 영역. 나머지 탐색 단추와 비슷한 방식으로 작동합니다.  
  
```vb
' Move to the first record in the bound Recordset.  
Sub First_OnClick  
   DC1.Recordset.MoveFirst  
End Sub  
  
' Move to the next record from the current position   
' in the bound Recordset.  
Sub Next_OnClick  
   If Not DC1.Recordset.EOF Then    ' Cannot move beyond bottom record.  
      DC1.Recordset.MoveNext  
      Exit Sub  
   End If     
End Sub  
  
' Move to the previous record from the current position in the bound   
' Recordset.  
Sub Prev_OnClick  
   If Not DC1.Recordset.BOF Then    ' Cannot move beyond top record.  
      DC1.Recordset.MovePrevious  
      Exit Sub  
   End If  
End Sub  
  
' Move to the last record in the bound Recordset.  
Sub Last_OnClick  
   DC1.Recordset.MoveLast  
End Sub  
```  
  
## <a name="see-also"></a>관련 항목  
 [DataControl 개체 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드(RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)



