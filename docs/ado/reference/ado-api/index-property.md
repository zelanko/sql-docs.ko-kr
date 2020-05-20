---
title: 인덱스 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset21::Index
helpviewer_keywords:
- Index property
ms.assetid: 1c79e271-21ec-41a8-8163-c5e89f0001a7
author: rothja
ms.author: jroth
ms.openlocfilehash: 2a77aa3c2e144859eaead332e71c5c4c8776608c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758699"
---
# <a name="index-property"></a>Index 속성
[레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체에 현재 적용 되는 인덱스의 이름을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 인덱스의 이름인 **문자열** 값을 설정 하거나 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **인덱스** 속성에 의해 명명 된 인덱스는 이전에 **레코드 집합** 개체의 기본 테이블에 선언 되어 있어야 합니다. 즉, 인덱스는 프로그래밍 방식으로 ADOX [인덱스](../../../ado/reference/adox-api/index-object-adox.md) 개체로 선언 되거나 기본 테이블이 생성 된 후에 선언 되어야 합니다.  
  
 인덱스를 설정할 수 없는 경우 런타임 오류가 발생 합니다. 다음 조건에서는 **인덱스** 속성을 설정할 수 없습니다.  
  
-   [WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md) 또는 **RecordsetChangeComplete** 이벤트 처리기 내에 있습니다.  
  
-   **레코드 집합** 에서 작업을 계속 실행 중인 경우 ( [상태](../../../ado/reference/ado-api/state-property-ado.md) 속성으로 확인할 수 있음)  
  
-   [필터 속성을](../../../ado/reference/ado-api/filter-property.md) 사용 하 여 **레코드 집합** 에 필터를 설정한 경우  
  
 **인덱스** 속성은 **레코드 집합** 을 닫을 경우 항상 성공적으로 설정 될 수 있지만, **레코드 집합이** 성공적으로 열리지 않거나, 기본 공급자가 인덱스를 지원 하지 않는 경우 인덱스를 사용할 수 없게 됩니다.  
  
 인덱스를 설정할 수 있는 경우 현재 행 위치가 변경 될 수 있습니다. 그러면 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) 속성을 업데이트 하 고 **WillChangeRecordset**, **RecordsetChangeComplete**, [WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)및 [MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md) 이벤트를 발생 시킵니다.  
  
 인덱스를 설정할 수 있고 [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) 속성이 **adlockpessimistic** 또는 **Adlockpessimistic**이면 암시적 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 연산이 수행 됩니다. 현재 및 영향을 받는 그룹을 해제 합니다. 기존 필터가 해제 되 고 현재 행 위치가 다시 정렬 된 **레코드 집합**의 첫 번째 행으로 변경 됩니다.  
  
 **Index** 속성은 [Seek](../../../ado/reference/ado-api/seek-method.md) 메서드와 함께 사용 됩니다. 기본 공급자가 **인덱스** 속성을 지원 하지 않으므로 **Seek** 메서드를 사용 하는 대신 [Find](../../../ado/reference/ado-api/find-method-ado.md) 메서드를 사용 하는 것이 좋습니다. **Recordset** 개체가 [supports](../../../ado/reference/ado-api/supports-method.md)**(adindex)** 메서드를 사용 하 여 인덱스를 지원 하는지 여부를 확인 합니다.  
  
 기본 제공 **인덱스** 속성은 모두 인덱스를 처리 하지만 dynamic [Optimize](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) 속성과는 관련이 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Seek 메서드 및 인덱스 속성 예제 (VB)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [Index 개체 (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)   
 [Seek 메서드](../../../ado/reference/ado-api/seek-method.md)
