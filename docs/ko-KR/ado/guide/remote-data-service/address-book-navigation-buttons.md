---
title: 주소록 탐색 단추 | Microsoft Docs
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
- RDS scenarios [ADO], navigation buttons
- address book application scenario [ADO], navigation buttons
ms.assetid: f0dd84c6-5c33-4ab9-82b4-4c42dfdd2277
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a98f56a876c8f7bf5712fb2a9cff90c5ddd0b96b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="address-book-navigation-buttons"></a>주소록 탐색 단추
주소록 응용 프로그램 웹 페이지의 맨 아래에 있는 탐색 단추를 표시합니다. 데이터의 첫 번째 또는 마지막 행 또는 현재 선택 영역에 인접 한 행 중 하나를 선택 하 여 HTML 눈금 표시의 데이터를 탐색 하려면 탐색 단추를 사용할 수 있습니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="navigation-sub-procedures"></a>탐색 Sub 프로시저  
 주소록 응용 프로그램에는 클릭 하 여 사용자가 허용 하는 여러 절차가 포함 되어는 **첫 번째**, **다음**, **이전**, 및 **마지막** 데이터를 이동 하는 단추입니다.  
  
 예를 들어,를 클릭 하 고 **첫 번째** 단추 VBScript First_OnClick Sub 프로시저를 활성화 합니다. 프로시저 실행을 [MoveFirst](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) 메서드를 현재 선택 영역 데이터의 첫 번째 행으로 만듭니다. 클릭 하는 **마지막** 호출 하는 Last_OnClick Sub 프로시저를 활성화 하는 단추는 [MoveLast](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) 데이터의 마지막 행 현재 선택 영역을 만드는 방법. 나머지 탐색 단추와 비슷한 방식에서 작동합니다.  
  
```  
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
  
## <a name="see-also"></a>관련 항목:  
 [DataControl 개체 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드(RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)



