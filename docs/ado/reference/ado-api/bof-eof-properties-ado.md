---
title: BOF, EOF 속성 (ADO) | Microsoft Docs
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
f1_keywords:
- Recordset15::BOF
- Recordset15::EOF
helpviewer_keywords:
- EOF property [ADO]
- BOF property [ADO]
ms.assetid: 36c31ab2-f3b6-4281-89b6-db7e04e38fd2
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1941b22639091d673bb687c3ae8b2d9ea1fdf063
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="bof-eof-properties-ado"></a>BOF, EOF 속성 (ADO)
-   **BOF** 현재 레코드 위치에 있는 첫 번째 레코드 앞에 있는 나타냅니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
-   **EOF** 여부를 지정 된 현재 레코드는 다음의 마지막 레코드는 **레코드 집합** 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 **BOF** 및 **EOF** 속성 반환 **부울** 값입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **BOF** 및 **EOF** 속성을 확인 여부는 **레코드 집합** 개체의 범위를 벗어났는지 여부 또는 레코드에 포함 되어는 **레코드 집합**  레코드 간을 이동할 때 개체입니다.  
  
 **BOF** 속성에서 반환 **True** (-1) 현재 레코드 위치는 첫 번째 레코드 바로 앞 이면 및 **False** 현재 레코드 위치는 첫 번째 이후인 경우 (0) 레코드입니다.  
  
 **EOF** 속성에서 반환 **True** 현재 레코드 위치 마지막 레코드 이후에 경우 및 **False** 위치가 있는 경우 현재 레코드 또는 마지막 레코드 이전 합니다.  
  
 경우는 **BOF** 또는 **EOF** 속성은 **True**, 현재 기록이 없습니다.  
  
 여는 경우는 **레코드 집합** 없는 레코드가 포함 된 개체는 **BOF** 및 **EOF** 속성으로 설정 됩니다 **True** (참조는 [ RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) 이 상태에 대 한 자세한 내용은 **레코드 집합**). 열 때는 **레코드 집합** 첫 번째 레코드 레코드가 하나 이상 포함 된 개체는 현재 레코드와 **BOF** 및 **EOF** 속성은 **False** .  
  
 마지막 남은 레코드를 삭제 하는 경우는 **레코드 집합** 개체는 **BOF** 및 **EOF** 속성 유지 **False** 할 때까지 현재 레코드의 위치를 변경 하려고 시도 합니다.  
  
 이 표에서 **이동** 의 다양 한 조합과 함께 메서드를 사용할 수는 **BOF** 및 **EOF** 속성입니다.  
  
||MoveFirst,<br /><br /> MoveLast|MovePrevious,<br /><br /> < 0 이동|Move 0|MoveNext<br /><br /> > 0 이동|  
|------|-----------------------------|---------------------------------|------------|-----------------------------|  
|**BOF**=**True**, **EOF**=**False**|허용함|오류|오류|허용함|  
|**BOF**=**False**, **EOF**=**True**|허용함|허용함|오류|오류|  
|둘 다 **True**|오류|오류|오류|오류|  
|둘 다 **False**|허용함|허용함|허용함|허용함|  
  
 허용는 **이동** 메서드 메서드는 레코드를 제대로 찾는 것은 보증 하지 않습니다; 지정 된 호출만 의미 **이동** 메서드 오류가 발생 하지 것입니다.  
  
 다음 표에서 어떻게 됩니까는 **BOF** 및 **EOF** 속성 설정을 호출 하면 다양 한 **이동** 메서드 하지만 없는 성공적으로 레코드를 찾을 수 있습니다.  
  
||BOF|EOF|  
|------|---------|---------|  
|**MoveFirst**, **MoveLast**|로 설정 **True**|로 설정 **True**|  
|**이동** 0|변경 내용 없음|변경 내용 없음|  
|**MovePrevious**, **Move** < 0|로 설정 **True**|변경 내용 없음|  
|**MoveNext**, **이동** > 0|변경 내용 없음|로 설정 **True**|  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [BOF, EOF, 및 책갈피 속성 예제 (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF, EOF, 및 책갈피 속성 예제 (VC + +)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
