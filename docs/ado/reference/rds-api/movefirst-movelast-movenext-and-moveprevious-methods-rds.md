---
description: MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드(RDS)
title: MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- MoveLast method [RDS]
- MovePrevious method [RDS]
- MoveFirst method [RDS]
- MoveNext method [RDS]
ms.assetid: 45c80bb5-136f-4204-9df2-78740fa55574
author: rothja
ms.author: jroth
ms.openlocfilehash: 151c111db94cd0132196437fc86e2aa9f80be7e8
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88768002"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-rds"></a>MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드(RDS)
지정 된 [레코드 집합](../ado-api/recordset-object-ado.md) 개체에서 첫 번째, 마지막, 다음 또는 이전 레코드로 이동 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataControl.Recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataControl*  
 RDS를 나타내는 개체 변수입니다 [. DataControl](./datacontrol-object-rds.md) 개체입니다.  
  
## <a name="remarks"></a>설명  
 RDS와 함께 **Move** 메서드를 사용할 수 있습니다 **. ** 웹 페이지에 있는 데이터 바인딩된 컨트롤의 데이터 레코드를 탐색 하는 DataControl 개체입니다. 예를 들어, RDS에 바인딩하여 **레코드 집합** 을 표로 표시 한다고 가정 **합니다. DataControl** 개체입니다. 그런 다음 사용자가 클릭 하 여 표시 된 **레코드 집합**에서 첫 번째, 마지막, 다음 또는 이전 레코드로 이동 하는 데 사용할 수 있는 첫 번째, 마지막, 다음 및 이전 단추를 포함할 수 있습니다. 이렇게 하려면 RDS의 **MoveFirst**, **MoveLast**, **MoveNext**및 **MovePrevious** 메서드를 호출 합니다 **. ** 각각의 첫 번째, 마지막, 다음 및 이전 단추에 대 한 onClick 프로시저의 DataControl 개체입니다. 주소록 [예제](../../guide/remote-data-service/address-book-navigation-buttons.md) 에서는이 작업을 수행 하는 방법을 보여 줍니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>참고 항목  
 [Move 메서드 (ADO)](../ado-api/move-method-ado.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (ADO)](../ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveRecord 메서드(ADO)](../ado-api/moverecord-method-ado.md)