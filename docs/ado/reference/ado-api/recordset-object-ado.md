---
title: 레코드 집합 개체 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset
helpviewer_keywords:
- Recordset object [ADO]
ms.assetid: ede1415f-c3df-4cc5-a05b-2576b2b84b60
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cc95d6ef7e61dcde373a646359d134dce0b3389d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711936"
---
# <a name="recordset-object-ado"></a>레코드 집합 개체(ADO)
기본 테이블 또는 실행 된 명령의 결과 레코드의 전체 집합을 나타냅니다. 언제 든 지 합니다 **레코드 집합** 개체를 현재 레코드로 집합 내에서 단일 레코드만 가리킵니다.  
  
## <a name="remarks"></a>Remarks  
 사용할 **레코드 집합** 공급자에서 데이터를 조작 하는 개체입니다. 거의 전적으로 사용 하 여 데이터를 조작 하는 ADO를 사용 하면 **레코드 집합** 개체입니다. 모든 **레코드 집합** 레코드 (행)의 개체를 구성 하 고 필드 (열). 공급자가 지 원하는 기능에 따라 일부 **레코드 집합** 메서드나 속성을 사용할 수 있습니다.  
  
 ADODB 합니다. 레코드 집합을 만들려면 사용할 ProgID를 **레코드 집합** 개체입니다. 오래 된 ADOR 참조 하는 기존 응용 프로그램입니다. 작업을 다시 컴파일하지 않고도 레코드 집합 ProgID는 계속 되지만 새로운 개발 ADODB 참조 해야 합니다. 레코드 집합입니다.  
  
 ADO에 정의 된 네 가지 다른 커서 유형을 가지합니다  
  
-   **동적 커서** 추가, 변경 및 삭제 하 여 다른 사용자가 볼 수 있습니다를 사용 하면 모든 유형의 통해 이동 합니다 **레코드 집합** 책갈피에 의존 하지 않습니다 하 고 공급자가 지 원하는 경우 책갈피를 수 있습니다. 해당 합니다.  
  
-   **키 집합 커서** 동적 커서를 사용 하면 레코드를 표시 합니다. 다른 사용자가 제외 하 고 같은 Behaves 추가한 다른 사용자가 삭제는 레코드에 대 한 액세스를 방지 합니다. 다른 사용자가 데이터 변경 내용을 계속 표시 됩니다. 항상 책갈피를 지원 하 고 되므로 모든 종류의를 통해 이동이 가능 합니다 **레코드 집합**합니다.  
  
-   **정적 커서** 정적 복사본 데이터를 찾거나 보고서를 생성 하는 데를 레코드 집합을 제공 하 고 책갈피를 항상 허용 되므로 모든 종류의를 통해 이동이 가능 합니다 **레코드 집합**합니다. 추가, 변경 또는 다른 사용자가 삭제 표시 되지 않습니다. 이 클라이언트 쪽을 열 때 허용 되는 커서 유형만 **레코드 집합** 개체입니다.  
  
-   **정방향 전용 커서** 앞 으로만 스크롤할 수 있습니다 합니다 **레코드 집합**합니다. 추가, 변경 또는 다른 사용자가 삭제 표시 되지 않습니다. 이 한 번 통과 해야 하는 경우에는 성능이 향상 된 **레코드 집합**합니다.  
  
 설정 합니다 [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) 열기 전에 속성을 **레코드 집합** 커서 유형을 선택 하거나 전달 하는 *CursorType* 인수를를 [엽니다](../../../ado/reference/ado-api/open-method-ado-recordset.md)메서드. 일부 공급자는 모든 커서 유형에 지원 하지 않습니다. 공급자에 대 한 설명서를 확인 합니다. 커서 유형을 지정 하지 않으면, ADO는 기본적으로 정방향 전용 커서를 엽니다.  
  
 경우는 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성이 **adUseClient** 열려는 **레코드 집합**의 **UnderlyingValue** 속성[필드](../../../ado/reference/ado-api/field-object.md) 반환 된 개체 불가능 **레코드 집합** 개체입니다. 일부 공급자 (예: OLE DB와 함께에서 Microsoft SQL server의 Microsoft ODBC 공급자)를 사용 하는 경우 만들 수 있습니다 **Recordset** 미리 정의 된 관계 없이 개체 [연결](../../../ado/reference/ado-api/connection-object-ado.md)연결 문자열을 전달 하 여 개체를 **Open** 메서드. 만드는 경우 ADO는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 하지만 개체를 개체 변수에 개체를 할당 하지 않습니다. 그러나 여러를 여는 경우 **레코드 집합** 명시적으로 만들를 열고 동일한 연결을 통해 개체를 **연결** 개체;이 할당 된 **연결**개체는 개체 변수입니다. 열 때이 개체 변수를 사용 하지 않는 프로그램 **레코드 집합** 개체를 새로 만들고 ADO **연결** 새 개체 각각에 대해 **레코드 집합**동일한 전달 하는 경우에, 연결 문자열입니다.  
  
 만큼 만들 수 있습니다 **레코드 집합** 필요에 따라 개체입니다.  
  
 여는 경우는 **레코드 집합**, 현재 레코드 (해당 되는 경우) 첫 번째 레코드에 배치 됩니다 및 [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 및 [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 속성으로 설정 됩니다 **False**. 레코드가 없는 경우는 **BOF** 하 고 **EOF** 속성 설정이 **True**합니다.  
  
 사용할 수는 [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), **MoveLast**를 **MoveNext**, 및 **MovePrevious** 메서드를 [이동](../../../ado/reference/ado-api/move-method-ado.md) 메서드 하며 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md), [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md), 및 [필터](../../../ado/reference/ado-api/filter-property.md) 속성 공급자가 지 원하는 관련 가정 하 여 현재 레코드의 위치를 변경 하려면 기능입니다. 앞 으로만 이동 가능한 **레코드 집합** 개체는만 지원 합니다 [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) 메서드. 사용 하는 경우는 **이동** 각 레코드를 방문 하는 방법 (열거 또는 합니다 **레코드 집합**)를 사용할 수는 **BOF** 및 **EOF** 속성을 시작 또는 끝을 지 나 이동 했으므로 경우를 확인 합니다 **레코드 집합**합니다.  
  
 모든 기능을 사용 하기 전에 **레코드 집합** 개체를 호출 해야 합니다는 **지원** 지원 되거나 사용할 수 있는 기능 인지 확인 하려면 개체의 메서드. 기능을 사용 하면 안 때 합니다 **지원** 메서드에서 false를 반환 합니다. 예를 들어 사용할 수 있습니다 합니다 **MovePrevious** 경우에만 메서드 `Recordset.Supports(adMovePrevious)` 반환 **True**합니다. 그렇지 않으면 오류가 표시 됩니다는, 때문에 합니다 **레코드 집합** 개체가 닫히지 않고 기능 인스턴스에서 사용할 수 없게 렌더링 합니다. 원하는 기능이 지원 되지 않는 경우 **지원** 도 false로 반환 됩니다. 해당 속성 또는 메서드를 호출 하지 않아야이 경우에 **레코드 집합** 개체입니다.  
  
 **레코드 집합** 개체를 업데이트 하는 두 가지 유형의 지원할 수 있습니다: 즉각적이 고 일괄 처리 합니다. 즉시 업데이트에서는 모든 데이터 변경 내용이 쓰는지 즉시 기본 데이터 원본에 호출 하 여 [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드. 값의 배열을 사용 하 여 매개 변수로 전달할 수도 있습니다는 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) 및 **업데이트** 메서드 및 동시에 레코드의 여러 필드를 업데이트 합니다.  
  
 공급자가 지 원하는 일괄 처리 업데이트를 할 수 있습니다 공급자에 둘 이상의 레코드 변경 내용을 캐시 하 고 사용 하 여 데이터베이스에 대 한 단일 호출에서 전송 해야 합니다 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드. 이 변경 사항이 적용 됩니다는 **AddNew**를 **업데이트**, 및 [삭제](../../../ado/reference/ado-api/delete-method-ado-recordset.md) 메서드. 호출한 후 합니다 **UpdateBatch** 메서드를 사용할 수는 [상태](../../../ado/reference/ado-api/status-property-ado-recordset.md) 속성을 해결 하기 위해 모든 데이터 충돌을 확인 합니다.  
  
> [!NOTE]
>  사용 하지 않고 쿼리를 실행 하는 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체, 쿼리 문자열을 전달 하는 **열기** 메서드를 **레코드 집합** 개체입니다. 그러나를 **명령** 개체는 명령 텍스트를 유지 하 고 다시 실행 하거나 쿼리 매개 변수를 사용 하려는 경우에 필요 합니다.  
  
 합니다 [모드](../../../ado/reference/ado-api/mode-property-ado.md) 속성은 액세스 권한을 제어 합니다.  
  
 **필드** 수집은의 기본 멤버는 **레코드 집합** 개체입니다. 결과적으로, 다음 두 코드 문은 동일합니다.  
  
```  
Debug.Print objRs.Fields.Item(0)  ' Both statements print   
Debug.Print objRs(0)              '  the Value of Item(0).  
```  
  
 경우는 **레코드 집합** 개체만 프로세스 간에 전달 되는 **행 집합** 값은 배열, 및 속성을는 **레코드 집합** 개체는 무시 됩니다. Unmarshalling, 하는 동안 합니다 **행 집합** 새로 만든으로 압축 되지 **레코드 집합** 도 기본 값으로 해당 속성을 설정 하는 개체입니다.  
  
 합니다 **레코드 집합** 개체가 스크립팅 작업에 안전 합니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [레코드 집합 개체 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/recordset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [필드 컬렉션 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Properties 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)
