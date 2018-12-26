---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3afc55ca26a8462eb5662287288ee885f9104a8c
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606691"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-rds"></a>MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드(RDS)
첫 번째, 마지막으로 이동의 지정 된 다음 또는 이전 레코드 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataControl.Recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataControl*  
 나타내는 개체 변수는 [rds. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 사용할 수는 **이동** 사용 하 여 메서드를 **rds. DataControl** 웹 페이지에서 데이터 바인딩된 컨트롤에 있는 데이터 레코드를 탐색 하는 개체입니다. 예를 들어, 표시 하는 **레코드 집합** 바인딩하여 표에 **rds. DataControl** 개체입니다. 사용자가 첫 번째 이동, 마지막으로, 다음을 클릭할 수 있는 첫 번째, 마지막으로, 다음 및 이전 단추를 포함할 수 있습니다 또는 표시 된 이전 레코드 **레코드 집합**합니다. 호출 하 여이 작업을 수행 합니다 **MoveFirst**, **MoveLast**를 **MoveNext**, 및 **MovePrevious** 메서드는 **rds. DataControl** 각각 onClick 절차에서는 첫 번째, 마지막으로, 다음 및 이전 단추에 대 한 개체입니다. 합니다 [주소록 예제](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md) 이 작업을 수행 하는 방법을 보여 줍니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>관련 항목  
 [Move 메서드 (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst, MoveLast, MoveNext 및 MovePrevious 메서드 (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveRecord 메서드(ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)


