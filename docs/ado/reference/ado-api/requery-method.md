---
description: Requery 메서드
title: Requery 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 12f60b295d569119a356631dc445bd034916665a
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989554"
---
# <a name="requery-method"></a>Requery 메서드
개체의 기반이 되는 쿼리를 다시 실행 하 여 [레코드 집합](./recordset-object-ado.md) 개체의 데이터를 업데이트 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.Requery Options  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Options*  
 선택 사항입니다. 이 작업에 영향을 주는 [Executeoptionenum](./executeoptionenum.md) 및 [CommandTypeEnum](./commandtypeenum.md) 값이 포함 된 비트 마스크입니다.  
  
> [!NOTE]
>  *옵션이* **adasyncexecute**로 설정 된 경우이 작업은 비동기적으로 실행 되며 종료 될 때 [RecordsetChangeComplete](./willchangerecordset-and-recordsetchangecomplete-events-ado.md) 이벤트가 발생 합니다. **AdExecuteNoRecords** 또는 **AdExecuteStream** 의 **Executeopenenum** 값은 **Requery**와 함께 사용 하면 안 됩니다.  
  
## <a name="remarks"></a>설명  
 **Requery** 메서드를 사용 하 여 원래 명령을 다시 시작 하 고 데이터를 두 번 검색 하 여 데이터 원본에서 **레코드 집합** 개체의 전체 내용을 새로 고칩니다. 이 메서드를 호출 하는 것은 [Close](./close-method-ado.md) 및 [Open](./open-method-ado-recordset.md) 메서드를 연속 해 서 호출 하는 것과 같습니다. 현재 레코드를 편집 하거나 새 레코드를 추가 하는 경우 오류가 발생 합니다.  
  
 **레코드 집합** 개체가 열려 있는 동안 커서의 특성을 정의 하는 속성 ([CursorType](./cursortype-property-ado.md), [LockType](./locktype-property-ado.md), [MaxRecords](./maxrecords-property-ado.md)등)은 읽기 전용입니다. 따라서 **Requery** 메서드는 현재 커서를 새로 고칠 수 있습니다. 커서 속성을 변경 하 고 결과를 보려면 [Close](./close-method-ado.md) 메서드를 사용 하 여 속성을 읽기/쓰기로 다시 만들어야 합니다. 그런 다음 속성 설정을 변경 하 고 [Open](./open-method-ado-recordset.md) 메서드를 호출 하 여 커서를 다시 열 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Execute, Requery 및 Clear 메서드 예제 (VB)](./execute-requery-and-clear-methods-example-vb.md)   
 [Execute, Requery 및 Clear 메서드 예제 (VBScript)](./execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute, Requery 및 Clear 메서드 예제 (VC + +)](./execute-requery-and-clear-methods-example-vc.md)   
 [CommandText 속성(ADO)](./commandtext-property-ado.md)