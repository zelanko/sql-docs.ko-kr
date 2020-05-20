---
title: Requery 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Requery
- Recordset15::raw_Requery
helpviewer_keywords:
- Requery method [ADO]
ms.assetid: d81ab76f-1aa8-4ccf-92ec-b65254dc3ea1
author: rothja
ms.author: jroth
ms.openlocfilehash: 29b2d0cba996e3f41a12df93babe8d9b86a8fbeb
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82756521"
---
# <a name="requery-method"></a>Requery 메서드
개체의 기반이 되는 쿼리를 다시 실행 하 여 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체의 데이터를 업데이트 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.Requery Options  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Options*  
 (선택 사항) 이 작업에 영향을 주는 [Executeoptionenum](../../../ado/reference/ado-api/executeoptionenum.md) 및 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 값이 포함 된 비트 마스크입니다.  
  
> [!NOTE]
>  *옵션이* **adasyncexecute**로 설정 된 경우이 작업은 비동기적으로 실행 되며 종료 될 때 [RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md) 이벤트가 발생 합니다. **AdExecuteNoRecords** 또는 **AdExecuteStream** 의 **Executeopenenum** 값은 **Requery**와 함께 사용 하면 안 됩니다.  
  
## <a name="remarks"></a>설명  
 **Requery** 메서드를 사용 하 여 원래 명령을 다시 시작 하 고 데이터를 두 번 검색 하 여 데이터 원본에서 **레코드 집합** 개체의 전체 내용을 새로 고칩니다. 이 메서드를 호출 하는 것은 [Close](../../../ado/reference/ado-api/close-method-ado.md) 및 [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드를 연속 해 서 호출 하는 것과 같습니다. 현재 레코드를 편집 하거나 새 레코드를 추가 하는 경우 오류가 발생 합니다.  
  
 **레코드 집합** 개체가 열려 있는 동안 커서의 특성을 정의 하는 속성 ([CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md), [LockType](../../../ado/reference/ado-api/locktype-property-ado.md), [MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)등)은 읽기 전용입니다. 따라서 **Requery** 메서드는 현재 커서를 새로 고칠 수 있습니다. 커서 속성을 변경 하 고 결과를 보려면 [Close](../../../ado/reference/ado-api/close-method-ado.md) 메서드를 사용 하 여 속성을 읽기/쓰기로 다시 만들어야 합니다. 그런 다음 속성 설정을 변경 하 고 [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드를 호출 하 여 커서를 다시 열 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Execute, Requery 및 Clear 메서드 예제 (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Execute, Requery 및 Clear 메서드 예제 (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute, Requery 및 Clear 메서드 예제 (VC + +)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CommandText 속성(ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)
