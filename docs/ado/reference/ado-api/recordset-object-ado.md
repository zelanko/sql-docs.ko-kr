---
title: 레코드 집합 개체 (ADO) | Microsoft Docs
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
- Recordset
helpviewer_keywords:
- Recordset object [ADO]
ms.assetid: ede1415f-c3df-4cc5-a05b-2576b2b84b60
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: fb2a9bee0cf7f092ffa30e1450dd11e34fd1eed1
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="recordset-object-ado"></a>레코드 집합 개체 (ADO)
기본 테이블이 나 실행 된 명령의 결과에서 레코드의 전체 집합을 나타냅니다. 언제 든 지는 **레코드 집합** 개체가 현재 레코드로 집합 내에서 단일 레코드로 참조 합니다.  
  
## <a name="remarks"></a>주의  
 사용 하면 **레코드 집합** 공급자에서 데이터를 조작 하는 개체입니다. 거의 전적으로 사용 하 여 데이터를 조작 하는 ADO를 사용 하면 **레코드 집합** 개체입니다. 모든 **레코드 집합** 개체 레코드 (행)으로 구성 하 고 필드 (열)입니다. 공급자가 지 원하는 기능에 따라 일부 **레코드 집합** 메서드 또는 속성을 사용할 수 있습니다.  
  
 ADODB 합니다. 레코드 집합을 만드는 데 사용할 해야 ProgID는 **레코드 집합** 개체입니다. 오래 된 ADOR 참조 하는 기존 응용 프로그램입니다. 을 다시 컴파일하지 않고 작동 하도록 ProgID 레코드 집합은 계속 되지만 새로운 개발 ADODB 참조 해야 합니다. 레코드 집합입니다.  
  
 ADO에 정의 된 4 개의 다른 커서 유형이 있습니다.  
  
-   **동적 커서** 사용 하면 모든 종류의를 통해 이동 추가, 변경 및 삭제; 다른 사용자가 볼 수 있습니다는 **레코드 집합** 책갈피;에 의존 하지 않도록 하 고 공급자가 지 원하는 경우 책갈피를 수 있습니다. 해당 합니다.  
  
-   **키 집합 커서** 동적 커서를 사용 하면 레코드 볼 다른 사용자가 제외 하 고 같은 Behaves 추가 하 고, 다른 사용자를 삭제 하는 레코드에 액세스할 수 있습니다. 다른 사용자가 데이터 변경 내용이 표시 됩니다. 항상 책갈피를 지원 하 고 모든 종류의를 통해 이동 되므로 가능는 **레코드 집합**합니다.  
  
-   **정적 커서** 사용 하 여 데이터를 검색 하거나 보고서를 생성 하는 레코드 집합의 정적 복사본을 제공 하 고 책갈피를 항상 허용 되므로 모든 종류의를 통해 이동이 가능는 **레코드 집합**합니다. 추가, 변경 또는 다른 사용자가 삭제 표시 되지 않습니다. 이 클라이언트 쪽을 열 때 허용 되는 커서 유형만 **레코드 집합** 개체입니다.  
  
-   **정방향 전용 커서** 앞 으로만 스크롤할 수 있습니다는 **레코드 집합**합니다. 추가, 변경 또는 다른 사용자가 삭제 표시 되지 않습니다. 이 경우에 한 번 통과 해야 하는 경우에는 성능이 향상 된 **레코드 집합**합니다.  
  
 설정의 [모두](../../../ado/reference/ado-api/cursortype-property-ado.md) 열기 전에 속성에서 **레코드 집합** 커서 유형을 선택 하거나 전달 하는 *모두* 인수를 사용는 [열](../../../ado/reference/ado-api/open-method-ado-recordset.md)메서드. 일부 공급자는 모든 커서 유형에 지원 하지 않습니다. 공급자에 대 한 설명서를 확인 합니다. 커서 유형을 지정 하지 않으면, ADO는 기본적으로 정방향 전용 커서를 엽니다.  
  
 경우는 [앞](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성이 **adUseClient** 열려는 **레코드 집합**, **UnderlyingValue** 속성[필드](../../../ado/reference/ado-api/field-object.md) 개체는 반환 된에서 사용할 수 없는 **레코드 집합** 개체입니다. 만들 수 있습니다 (예: OLE DB 함께에서 Microsoft SQL server 용 Microsoft ODBC 공급자)는 일부 공급자를 사용할 때는 **레코드 집합** 객체를 개별적으로 이전에 정의한 [연결](../../../ado/reference/ado-api/connection-object-ado.md)연결 문자열을 전달 하 여 개체는 **열려** 메서드. ADO 만듭니다는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 해당 개체는 개체 변수를 할당 하지 않습니다. 그러나 여러를 여는 경우 **레코드 집합** 명시적으로 만들고이 열에 동일한 연결을 통해 개체는 **연결** 개체;이 할당의 **연결**개체 변수에 개체입니다. 열 때이 개체 변수를 사용 하지 않는 프로그램 **레코드 집합** 개체, ADO 원본 또는 **연결** 각각에 대 한 개체를 새 **레코드 집합**동일한 전달 하는 경우에, 연결 문자열입니다.  
  
 만큼 만들 수 있습니다 **레코드 집합** 필요에 따라 개체입니다.  
  
 열 때는 **레코드 집합**는 현재 레코드 (해당 되는 경우) 첫 번째 레코드에 위치 및 [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 및 [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 속성으로 설정 됩니다 **False**. 레코드가 없는 경우는 **BOF** 및 **EOF** 속성 설정이 **True**합니다.  
  
 사용할 수는 [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), **MoveLast**, **MoveNext**, 및 **MovePrevious** 메서드; [이동](../../../ado/reference/ado-api/move-method-ado.md) 메서드도 있습니다. 및 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md), [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md), 및 [필터](../../../ado/reference/ado-api/filter-property.md) 관련 공급자가 지 원하는 것으로 가정 하 여 현재 레코드의 위치를 변경 하는 속성 기능입니다. 앞 으로만 이동 가능한 **레코드 집합** 개체 지원만 [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) 메서드. 사용 하는 경우는 **이동** 각 레코드를 방문 하는 메서드 (하거나 열거는 **레코드 집합**)를 사용할 수 있습니다는 **BOF** 및 **EOF** 속성을 시작 또는 끝을 지 나 이동 하는 경우 확인 된 **레코드 집합**합니다.  
  
 모든 기능을 사용 하기 전에 **레코드 집합** 개체를 호출 해야 합니다는 **지원** 메서드를 사용할 수 없거나 지원 되는 기능 인지 확인 하는 개체입니다. 기능을 사용 하지 않아야 때는 **지원** 메서드에서 false를 반환 합니다. 예를 들어, 사용할 수는 **MovePrevious** 경우에만 메서드 `Recordset.Supports(adMovePrevious)` 반환 **True**합니다. 그렇지 않으면 얻게 됩니다 오류가 발생 하기 때문에 **레코드 집합** 개체가 잠겨 되 고 기능 인스턴스를 사용할 수 없도록 렌더링 합니다. 기능에 관심이 있는 지원 되지 않는 경우 **지원** 도 false 반환 합니다. 에 해당 속성이 나 메서드를 호출 하지 않아야이 경우에 **레코드 집합** 개체입니다.  
  
 **레코드 집합** 개체를 업데이트 하는 두 가지 유형의 지원할 수 있습니다: 즉시 및 일괄 처리 합니다. 즉시 업데이트에 모든 데이터 변경은 즉시 기록 기본 데이터 원본에 호출 하 여 [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드. 값의 배열을와 매개 변수로 전달할 수도 있습니다는 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) 및 **업데이트** 메서드 및 동시에 레코드의 여러 필드를 업데이트 합니다.  
  
 공급자는 일괄 처리 업데이트를 지 원하는 공급자에 둘 이상의 레코드 변경 내용을 캐시 하 고 사용 하 여 데이터베이스를 한 번 호출에 전송 하도록 할 수 있습니다는 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드. 이 변경 된 내용에 적용 됩니다는 **AddNew**, **업데이트**, 및 [삭제](../../../ado/reference/ado-api/delete-method-ado-recordset.md) 메서드. 호출한 후는 **UpdateBatch** 사용할 수는 [상태](../../../ado/reference/ado-api/status-property-ado-recordset.md) 데이터 충돌에 대 한 문제를 해결 하기 위해 확인할 속성입니다.  
  
> [!NOTE]
>  사용 하지 않고 쿼리를 실행 하는 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체에 쿼리 문자열을 전달 하는 **열려** 의 메서드는 **레코드 집합** 개체입니다. 그러나 한 **명령** 명령 텍스트를 유지 하 고 했다가 나중에 다시 실행 하거나 쿼리 매개 변수를 사용 하려는 경우 개체가 필요 합니다.  
  
 [모드](../../../ado/reference/ado-api/mode-property-ado.md) 속성은 액세스 권한을 제어 합니다.  
  
 **필드** 컬렉션은의 기본 멤버는 **레코드 집합** 개체입니다. 결과적으로, 다음 두 코드 문은 동일합니다.  
  
```  
Debug.Print objRs.Fields.Item(0)  ' Both statements print   
Debug.Print objRs(0)              '  the Value of Item(0).  
```  
  
 경우는 **레코드 집합** 개체 프로세스 에서만 전반에서 전달 되는 **행 집합** 값을 마샬링의 속성과 **레코드 집합** 개체는 무시 됩니다. Unmarshalling, 하는 동안는 **행 집합** 새로 만든에 압축을 풀 **레코드 집합** 개체도 해당 속성을 기본값으로 설정 하는 것입니다.  
  
 **레코드 집합** 개체는 스크립팅 작업에 안전 합니다.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [레코드 집합 개체 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/recordset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Fields 컬렉션 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Properties 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)
