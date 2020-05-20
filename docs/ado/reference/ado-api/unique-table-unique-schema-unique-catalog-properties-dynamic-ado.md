---
title: 레코드 집합 기본 테이블의 변경 내용 제어 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Unique Table property [ADO]
- Unique Schema property [ADO]
- Unique Catalog property [ADO]
ms.assetid: d0e775d8-e353-46a1-ad10-ed4cc240dfaa
author: rothja
ms.author: jroth
ms.openlocfilehash: ac7fa0cf50a92b2738d3e83d5e7b9d5fac46fd9b
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759519"
---
# <a name="unique-table-unique-schema-unique-catalog-properties-dynamic-ado"></a>고유 테이블, 고유 스키마, 고유 카탈로그 속성-동적 (ADO)
를 사용 하면 여러 기본 테이블에 대 한 조인 작업으로 구성 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 의 특정 기본 테이블에 대 한 수정을 엄격 하 게 제어할 수 있습니다.  
  
-   **고유 테이블** 업데이트, 삽입 및 삭제를 허용 하는 기본 테이블의 이름을 지정 합니다.  
  
-   **Unique 스키마** 테이블 소유자의 *스키마*또는 이름을 지정 합니다.  
  
-   **고유 카탈로그** 테이블을 포함 하는 데이터베이스 이름 또는 *카탈로그*를 지정 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 테이블, 스키마 또는 카탈로그의 이름인 **문자열** 값을 설정 하거나 반환 합니다.  
  
## <a name="remarks"></a>설명  
 원하는 기본 테이블은 해당 카탈로그, 스키마 및 테이블 이름으로 고유 하 게 식별 됩니다. **Unique table** 속성이 설정 되 면 **고유 스키마** 또는 **고유한 카탈로그** 속성의 값을 사용 하 여 기본 테이블을 찾습니다. 고유 **테이블** 속성을 설정 하기 전에 **고유 스키마** 와 고유 **카탈로그** 속성 중 하나 또는 둘 모두를 설정 하는 것은 필수는 아닙니다.  
  
 **고유 테이블** 의 기본 키는 전체 **레코드 집합**의 기본 키로 처리 됩니다. 기본 키가 필요한 모든 메서드에 사용 되는 키입니다.  
  
 **Unique 테이블** 을 설정 하는 동안에는 [Delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md) 메서드가 명명 된 테이블에만 영향을 줍니다. [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md), [Resync](../../../ado/reference/ado-api/resync-method.md), [Update](../../../ado/reference/ado-api/update-method.md)및 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드는 **레코드 집합**의 적절 한 기본 테이블에 영향을 줍니다.  
  
 사용자 지정 재 동기화를 수행 하기 전에 **고유 테이블** 을 지정 해야 합니다. **Unique Table** 을 지정 하지 않은 경우 [Resync Command](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md) 속성은 아무런 영향을 주지 않습니다.  
  
 고유 기본 테이블을 찾을 수 없는 경우 런타임 오류가 발생 합니다.  
  
 이러한 동적 속성은 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성이 **adUseClient**로 설정 된 경우 **레코드 집합** 개체 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션에 모두 추가 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
