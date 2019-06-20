---
title: BOF, EOF 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::BOF
- Recordset15::EOF
helpviewer_keywords:
- EOF property [ADO]
- BOF property [ADO]
ms.assetid: 36c31ab2-f3b6-4281-89b6-db7e04e38fd2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9a449c0e635c7fe0e63bc1f4d8b1b0b91712135d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66696282"
---
# <a name="bof-eof-properties-ado"></a>BOF, EOF 속성(ADO)
-   **BOF** 레코드의 현재 위치에서 첫 번째 레코드 앞에 있는 나타냅니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
-   **EOF** 레코드의 현재 위치에 있는 마지막 레코드 뒤에 오는 나타냅니다는 **레코드 집합** 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 합니다 **BOF** 하 고 **EOF** 속성 반환 **부울** 값입니다.  
  
## <a name="remarks"></a>Remarks  
 사용 하 여는 **BOF** 및 **EOF** 속성을 확인 하는지 여부를 **레코드 집합** 개체에 레코드 또는 한도 범위를 벗어났는지 여부를 **레코드 집합**  레코드 간을 이동할 때 개체입니다.  
  
 합니다 **BOF** 속성이 반환 **True** (-1) 현재 레코드 위치가 첫 번째 레코드 앞 이면 및 **False** 현재 레코드 위치가 첫 번째 이후인 경우 (0) 레코드입니다.  
  
 **EOF** 속성에서 반환 **True** 마지막 레코드 다음 레코드 현재 위치 하는 경우 및 **False** 인지 레코드의 현재 위치에서 마지막 레코드 앞입니다.  
  
 경우는 **BOF** 하거나 **EOF** 속성은 **True**, 현재 레코드가 없습니다.  
  
 열면를 **레코드 집합** 없는 레코드를 포함 하는 개체를 **BOF** 하 고 **EOF** 속성으로 설정 됩니다 **True** (참조를 [ RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) 이 상태에 대 한 자세한 내용은 속성을 **레코드 집합**). 여는 경우는 **레코드 집합** 첫 번째 레코드를 하나 이상의 레코드를 포함 하는 개체는 현재 레코드와 **BOF** 및 **EOF** 속성은 **False** .  
  
 마지막 남은 레코드를 삭제 하는 경우는 **레코드 집합** 개체를 **BOF** 및 **EOF** 속성 유지 **False** 할 때까지 현재 레코드의 위치를 변경 하려고 시도 합니다.  
  
 이 표에서 **이동** 메서드를 가진 여러 조합으로 사용할 수는 **BOF** 하 고 **EOF** 속성입니다.  
  
||MoveFirst,<br /><br /> MoveLast|MovePrevious,<br /><br /> Move < 0|0 이동|MoveNext<br /><br /> > 0 이동|  
|------|-----------------------------|---------------------------------|------------|-----------------------------|  
|**BOF**=**True**, **EOF**=**False**|허용함|Error|Error|허용함|  
|**BOF**=**False**, **EOF**=**True**|허용함|허용함|Error|Error|  
|둘 다 **True**|Error|Error|Error|Error|  
|둘 다 **False**|허용함|허용함|허용함|허용함|  
  
 허용 된 **이동** 메서드는 메서드는 레코드를 제대로 찾는 것은 보장 하지 않으면 호출 된 것만 의미 **이동** 메서드는 오류가 생성 되지 것입니다.  
  
 다음 표에서 어떻게 되나요 합니다 **BOF** 하 고 **EOF** 속성 설정을 호출 하면 다양 한 **이동** 메서드 하지만 수 없는 레코드를 제대로 찾는 합니다.  
  
||BOF|EOF|  
|------|---------|---------|  
|**MoveFirst**, **MoveLast**|로 **True**|로 **True**|  
|**이동** 0|변경 안 함|변경 안 함|  
|**MovePrevious**, **Move** < 0|로 **True**|변경 안 함|  
|**MoveNext**, **Move** > 0|변경 안 함|로 **True**|  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [BOF, EOF 및 책갈피 속성 예제 (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF, EOF 및 책갈피 속성 예제 (VC + +)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
