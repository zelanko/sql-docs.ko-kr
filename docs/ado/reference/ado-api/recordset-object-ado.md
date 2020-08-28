---
description: 레코드 집합 개체(ADO)
title: 레코드 집합 개체 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: ff23c57ae3ecf25e7328d304f9716ad24f2aba7e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989743"
---
# <a name="recordset-object-ado"></a>레코드 집합 개체(ADO)
기본 테이블의 전체 레코드 집합 또는 실행 된 명령의 결과를 나타냅니다. 언제 든 지 **레코드 집합** 개체는 집합 내의 단일 레코드만 현재 레코드로 참조 합니다.  
  
## <a name="remarks"></a>설명  
 **레코드 집합** 개체를 사용 하 여 공급자의 데이터를 조작할 수 있습니다. ADO를 사용 하는 경우 **레코드 집합** 개체를 사용 하 여 거의 완전히 데이터를 조작 합니다. 모든 **레코드 집합** 개체는 레코드 (행)와 필드 (열)로 구성 됩니다. 공급자가 지 원하는 기능에 따라 일부 **레코드 집합** 메서드 또는 속성을 사용 하지 못할 수도 있습니다.  
  
 ADODB.DLL. 레코드 집합은 **레코드 집합** 개체를 만드는 데 사용 해야 하는 ProgID입니다. 오래 된 ADOR를 참조 하는 기존 응용 프로그램입니다. 레코드 집합 ProgID는 다시 컴파일하지 않고 계속 작동 하지만 새 개발은 ADODB를 참조 해야 합니다. 집합인.  
  
 ADO에는 다음과 같은 네 가지 커서 형식이 정의 되어 있습니다.  
  
-   **동적 커서** 다른 사용자가 추가, 변경 및 삭제 하는 것을 볼 수 있습니다. 책갈피를 사용 하지 않는 **레코드 집합** 을 통과 하는 모든 유형의 이동을 허용 합니다. 및는 공급자가 책갈피를 지 원하는 경우 책갈피를 허용 합니다.  
  
-   **키 집합 커서** 는 다른 사용자가 추가 하는 레코드를 볼 수 없도록 하 고 다른 사용자가 삭제 하는 레코드에 대 한 액세스를 방지 하는 것을 제외 하 고는 동적 커서 처럼 동작 합니다. 다른 사용자의 데이터 변경 내용은 계속 표시 됩니다. 항상 책갈피를 지원 하므로 **레코드 집합**을 통해 모든 유형의 이동이 가능 합니다.  
  
-   **정적 커서** 데이터를 찾거나 보고서를 생성 하는 데 사용할 레코드 집합의 정적 복사본을 제공 합니다. 항상 책갈피를 허용 하므로 **레코드 집합**을 통해 모든 유형의 이동을 허용 합니다. 다른 사용자에의 한 추가, 변경 또는 삭제는 표시 되지 않습니다. 클라이언트 쪽 **레코드 집합** 개체를 열 때 유일 하 게 허용 되는 커서 유형입니다.  
  
-   **앞 으로만 이동 가능한 커서** **레코드 집합**을 통해 앞 으로만 스크롤할 수 있습니다. 다른 사용자에의 한 추가, 변경 또는 삭제는 표시 되지 않습니다. 이렇게 하면 **레코드 집합**을 통과 하는 한 번만 수행 해야 하는 경우 성능이 향상 됩니다.  
  
 **레코드 집합** 을 열기 전에 [CursorType](./cursortype-property-ado.md) 속성을 설정 하 여 커서 유형을 선택 하거나 *CursorType* 인수를 [Open](./open-method-ado-recordset.md) 메서드로 전달 합니다. 일부 공급자는 모든 커서 유형을 지원 하지 않습니다. 공급자에 대 한 설명서를 확인 합니다. 커서 유형을 지정 하지 않으면 기본적으로 ADO에서 앞 으로만 이동 가능한 커서를 엽니다.  
  
 [CursorLocation](./cursorlocation-property-ado.md) 속성을 **adUseClient** 로 설정 하 여 **레코드 집합**을 여는 경우에는 [필드](./field-object.md) 개체의 **UnderlyingValue** 속성을 반환 된 **레코드 집합** 개체에서 사용할 수 없습니다. 일부 공급자 (예: Microsoft SQL Server와 함께 OLE DB 용 Microsoft ODBC 공급자)와 함께 사용 하는 경우에는 연결 문자열을 **Open** 메서드로 전달 하 여 이전에 정의한 [연결](./connection-object-ado.md) 개체와 독립적으로 **레코드 집합** 개체를 만들 수 있습니다. ADO는 여전히 [연결](./connection-object-ado.md) 개체를 만들지만 개체 변수에는 해당 개체를 할당 하지 않습니다. 그러나 같은 연결을 통해 **레코드 집합** 개체를 여러 개 여는 경우에는 명시적으로 **연결** 개체를 만들고 열어야 합니다. 그러면 **연결** 개체가 개체 변수에 할당 됩니다. **레코드 집합** 개체를 열 때이 개체 변수를 사용 하지 않는 경우 ADO는 동일한 연결 문자열을 전달 하더라도 각 새 **레코드 집합**에 대 한 새 **연결** 개체를 만듭니다.  
  
 필요한 만큼 **레코드 집합** 개체를 만들 수 있습니다.  
  
 **레코드 집합**을 열 때 현재 레코드는 첫 번째 레코드 (있는 경우)에 배치 되 고, [BOF](./bof-eof-properties-ado.md) 및 [EOF](./bof-eof-properties-ado.md) 속성은 **False**로 설정 됩니다. 레코드가 없는 경우에는 **BOF** 및 **EOF** 속성 설정이 **True**입니다.  
  
 [MoveFirst](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md), **MoveLast**, **MoveNext**및 **MovePrevious** 메서드를 사용할 수 있습니다. [Move](./move-method-ado.md) 메서드 그리고 [AbsolutePosition](./absoluteposition-property-ado.md), [AbsolutePage](./absolutepage-property-ado.md)및 [필터](./filter-property.md) 속성을 통해 현재 레코드의 위치를 변경할 수 있습니다 .이 경우 공급자가 관련 기능을 지 원하는 것으로 가정 합니다. 앞 으로만 이동 가능한 **레코드 집합** 개체는 [MoveNext](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md) 메서드만 지원 합니다. **Move** 메서드를 사용 하 여 각 레코드를 방문 하거나 레코드 **집합**을 열거 하는 경우에는 **BOF** 및 **EOF** 속성을 사용 하 여 **레코드 집합**의 시작 또는 끝을 넘어 이동 했는지 확인할 수 있습니다.  
  
 **레코드 집합** 개체의 기능을 사용 하기 전에 개체의 **Supports** 메서드를 호출 하 여 기능이 지원 되는지 또는 사용 가능한 지 확인 해야 합니다. **지원** 메서드가 false를 반환 하는 경우에는이 기능을 사용 하지 않아야 합니다. 예를 들어,가 True를 반환 하는 경우에만 **MovePrevious** 메서드를 사용할 수 있습니다 `Recordset.Supports(adMovePrevious)` . **True** 그렇지 않은 경우에는 **레코드 집합** 개체가 닫혀 있을 수 있으며 기능을 인스턴스에서 사용할 수 없기 때문에 오류가 발생 합니다. 관심이 있는 기능이 지원 되지 않는 경우에서 **지원** 되는 경우에도 false를 반환 합니다. 이 경우 **레코드 집합** 개체에 대해 해당 속성 또는 메서드를 호출 하지 않아야 합니다.  
  
 **레코드 집합** 개체는 즉시 실행 되 고 일괄 처리 되는 두 가지 유형의 업데이트를 지원할 수 있습니다. 즉시 업데이트에서 [Update](./update-method.md) 메서드를 호출 하면 데이터에 대 한 모든 변경 내용이 기본 데이터 소스에 즉시 기록 됩니다. [AddNew](./addnew-method-ado.md) 및 **Update** 메서드를 사용 하 여 값 배열을 매개 변수로 전달 하 고 레코드의 여러 필드를 동시에 업데이트할 수도 있습니다.  
  
 공급자에서 일괄 업데이트를 지 원하는 경우 공급자가 둘 이상의 레코드에 대 한 변경 내용을 캐시 한 다음 [UpdateBatch](./updatebatch-method.md) 메서드를 사용 하 여 데이터베이스에 대 한 단일 호출로 전송할 수 있습니다. 이는 **AddNew**, **Update**및 [Delete](./delete-method-ado-recordset.md) 메서드를 사용 하 여 변경한 내용에 적용 됩니다. **UpdateBatch** 메서드를 호출한 후 [Status](./status-property-ado-recordset.md) 속성을 사용 하 여 문제를 해결 하기 위해 데이터 충돌을 확인할 수 있습니다.  
  
> [!NOTE]
>  [명령](./command-object-ado.md) 개체를 사용 하지 않고 쿼리를 실행 하려면 **레코드 집합** 개체의 **Open** 메서드에 쿼리 문자열을 전달 합니다. 그러나 명령 텍스트를 유지 하 고 다시 실행 하거나 쿼리 매개 변수를 사용 하려는 경우에는 **command** 개체가 필요 합니다.  
  
 [Mode](./mode-property-ado.md) 속성은 액세스 권한을 제어 합니다.  
  
 **Fields** 컬렉션은 **레코드 집합** 개체의 기본 멤버입니다. 따라서 다음 두 코드 문은 동일 합니다.  
  
```  
Debug.Print objRs.Fields.Item(0)  ' Both statements print   
Debug.Print objRs(0)              '  the Value of Item(0).  
```  
  
 **레코드 집합** 개체가 여러 프로세스에 전달 되 면 **행** 집합 값만 배열 되 고 **recordset** 개체의 속성은 무시 됩니다. Unmarshalling 수행 하는 동안 **행 집합** 은 새로 만든 **레코드 집합** 개체에 압축을 풀고 해당 속성도 기본값으로 설정 됩니다.  
  
 **레코드 집합** 개체는 스크립팅에 안전 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [Recordset 개체 속성, 메서드 및 이벤트](./recordset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Connection 개체 (ADO)](./connection-object-ado.md)   
 [Fields 컬렉션 (ADO)](./fields-collection-ado.md)   
 [Properties 컬렉션 (ADO)](./properties-collection-ado.md)   
 [부록 A: 공급자](../../guide/appendixes/appendix-a-providers.md)