---
title: MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (RDS) | Microsoft Docs
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
apitype: COM
helpviewer_keywords:
- MoveLast method [RDS]
- MovePrevious method [RDS]
- MoveFirst method [RDS]
- MoveNext method [RDS]
ms.assetid: 45c80bb5-136f-4204-9df2-78740fa55574
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db7953e67e5ad7ed7cda0d4ba4afe077256cafc0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-rds"></a>MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (RDS)
첫 번째, 마지막으로 이동의 지정 된 다음 또는 이전 레코드 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataControl.Recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataControl*  
 개체 변수를 나타내는 [.rds입니다 DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체입니다.  
  
## <a name="remarks"></a>주의  
 사용할 수는 **이동** 있는 메서드는 **.rds입니다 DataControl** 웹 페이지에 데이터 바인딩된 컨트롤의 데이터 레코드를 탐색 하는 개체입니다. 예를 들어, 표시는 **레코드 집합** 에 바인딩하여 표에 **.rds입니다 DataControl** 개체입니다. 그런 다음 사용자가을 첫 번째 이동, 마지막, 다음을 클릭할 수 있는 First, Last, 다음을와 이전 단추를 포함할 수 또는 표시 된의 이전 레코드 **레코드 집합**합니다. 호출 하 여이 작업을 수행는 **MoveFirst**, **MoveLast**, **MoveNext**, 및 **MovePrevious** 의 메서드는 **.rds입니다 DataControl** 개체 First, Last, 다음을와 이전 하는 단추를 각각. [주소록 예제](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md) 이 작업을 수행 하는 방법을 보여 줍니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Move 메서드 (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveRecord 메서드(ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)


