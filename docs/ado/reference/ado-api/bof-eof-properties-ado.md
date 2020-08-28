---
description: BOF, EOF 속성(ADO)
title: BOF, EOF 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 710a116e28a102eeac8a7a062a9f66cd8dcbe79c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975784"
---
# <a name="bof-eof-properties-ado"></a>BOF, EOF 속성(ADO)
-   **BOF** 현재 레코드 위치가 [레코드 집합](./recordset-object-ado.md) 개체의 첫 번째 레코드 앞에 있음을 나타냅니다.  
  
-   **EOF** 현재 레코드 위치가 **레코드 집합** 개체의 마지막 레코드 뒤에 있음을 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
 **BOF** 및 **EOF** 속성은 **부울** 값을 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **BOF** 및 **EOF** 속성을 사용 하 여 레코드에서 레코드로 이동할 때 **레코드 집합 개체** 의 제한을 초과 했는지 여부를 확인할 수 **Recordset** 있습니다.  
  
 현재 레코드 위치가 첫 번째 레코드 앞에 있으면 **BOF** 속성은 **True** (-1)를 반환 하 고 현재 레코드 위치가 첫 번째 레코드에 있거나 첫 번째 레코드 뒤에 있으면 **False** (0)를 반환 합니다.  
  
 **EOF** 속성은 현재 레코드 위치가 마지막 레코드 뒤에 있으면 **True** 를 반환 하 고 현재 레코드 위치가 마지막 레코드 앞에 있으면 **False** 를 반환 합니다.  
  
 **BOF** 또는 **EOF** 속성이 **True**이면 현재 레코드가 없습니다.  
  
 레코드를 포함 하지 않는 **레코드 집합** 개체를 여는 경우에는 **BOF** 및 **EOF** 속성이 **True** 로 설정 됩니다 .이 **레코드 집합**상태에 대 한 자세한 내용은 [RecordCount](./recordcount-property-ado.md) 속성을 참조 하세요. 하나 이상의 레코드를 포함 하는 **레코드 집합** 개체를 열 때 첫 번째 레코드는 현재 레코드이 고, **BOF** 및 **EOF** 속성은 **False**입니다.  
  
 **레코드 집합** 개체에서 마지막으로 남아 있는 레코드를 삭제 하는 경우 현재 레코드의 위치를 변경할 때까지 **BOF** 및 **EOF** 속성이 **False로** 유지 될 수 있습니다.  
  
 다음 표에서는 다양 한 **BOF** 및 **EOF** 속성 조합을 사용 하 여 허용 되는 **이동** 메서드를 보여 줍니다.  
  
||MoveFirst<br /><br /> MoveLast|MovePrevious<br /><br /> Move < 0|0 이동|MoveNext<br /><br /> Move > 0|  
|------|-----------------------------|---------------------------------|------------|-----------------------------|  
|**BOF** = **True**, **EOF** = **False**|허용됨|Error|Error|허용됨|  
|**BOF** = **False**, **EOF** = **True**|허용됨|허용됨|Error|Error|  
|모두 **True**|Error|Error|Error|Error|  
|모두 **False**|허용됨|허용됨|허용됨|허용됨|  
  
 **Move** 메서드를 허용 해도 메서드가 레코드를 성공적으로 찾을 수 있도록 보장 하는 것은 아닙니다. 이는 지정 된 **Move** 메서드를 호출 해도 오류가 생성 되지 않는다는 것을 의미 합니다.  
  
 다음 표에서는 다양 한 **Move** 메서드를 호출 하지만 레코드를 찾을 수 없는 경우에 발생 하는 **BOF** 및 **EOF** 속성 설정을 보여 줍니다.  
  
||BOF|EOF|  
|------|---------|---------|  
|**MoveFirst**, **MoveLast**|**True** 로 설정|**True** 로 설정|  
|0 **이동**|변경 내용 없음|변경 내용 없음|  
|**MovePrevious**, **Move** < 0|**True** 로 설정|변경 내용 없음|  
|**MoveNext**, **Move** > 0|변경 내용 없음|**True** 로 설정|  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [BOF, EOF 및 Bookmark 속성 예제 (VB)](./bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF, EOF 및 Bookmark 속성 예제 (VC + +)](./bof-eof-and-bookmark-properties-example-vc.md)