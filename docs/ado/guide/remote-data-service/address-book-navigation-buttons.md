---
description: 주소록 탐색 단추
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 03959b22d0b64f2932326c42f5bb0117441b9051
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88758653"
---
# <a name="address-book-navigation-buttons"></a>주소록 탐색 단추
주소록 응용 프로그램은 웹 페이지의 맨 아래에 탐색 단추를 표시 합니다. 탐색 단추를 사용 하 여 데이터의 첫 번째 또는 마지막 행을 선택 하거나 현재 선택 영역에 인접 한 행을 선택 하 여 HTML 그리드 표시의 데이터를 탐색할 수 있습니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="navigation-sub-procedures"></a>탐색 하위 프로시저  
 주소록 응용 프로그램에는 사용자가 **첫 번째**, **다음**, **이전**및 **마지막** 단추를 클릭 하 여 데이터를 이동할 수 있도록 하는 몇 가지 절차가 포함 되어 있습니다.  
  
 예를 들어 **첫 번째** 단추를 클릭 하면 VBScript First_OnClick Sub 프로시저가 활성화 됩니다. 이 프로시저는 [MoveFirst](../../reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) 메서드를 실행 하 여 첫 번째 데이터 행을 현재 선택 항목으로 만듭니다. **마지막** 단추를 클릭 하면 Last_OnClick Sub 프로시저가 활성화 됩니다 .이 프로시저는 [MoveLast](../../reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) 메서드를 호출 하 여 마지막 데이터 행을 현재 선택 영역으로 만듭니다. 나머지 탐색 단추는 비슷한 방식으로 작동 합니다.  
  
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
 [DataControl 개체 (RDS)](../../reference/rds-api/datacontrol-object-rds.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드(RDS)](../../reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)