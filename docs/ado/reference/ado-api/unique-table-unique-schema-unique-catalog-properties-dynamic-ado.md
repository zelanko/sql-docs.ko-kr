---
title: "컨트롤 (ADO) 레코드 집합 기본 테이블에 변경 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Unique Table property [ADO]
- Unique Schema property [ADO]
- Unique Catalog property [ADO]
ms.assetid: d0e775d8-e353-46a1-ad10-ed4cc240dfaa
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 29120a3012b74196e9184384fc740b7c18363e98
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="unique-table-unique-schema-unique-catalog-properties-dynamic-ado"></a>고유 테이블, 고유 고유한 스키마 카탈로그 속성 동적 (ADO)
특정 기본 테이블에 제어 수정 밀접 하 게 할 수 있습니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 여러 기본 테이블에서 조인 작업으로 만든입니다.  
  
-   **고유 테이블** 는 업데이트, 삽입 및 삭제는 사용할 수는 기본 테이블의 이름을 지정 합니다.  
  
-   **고유한 스키마** 지정는 *스키마*, 또는 테이블의 소유자 이름입니다.  
  
-   **고유한 카탈로그** 지정는 *카탈로그*, 또는 테이블이 포함 된 데이터베이스의 이름입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **문자열** 값은 테이블, 스키마 또는 카탈로그의 이름입니다.  
  
## <a name="remarks"></a>주의  
 원하는 기본 테이블은 고유 하 게 해당 카탈로그, 스키마 및 테이블 이름으로 식별 됩니다. 때는 **고유 테이블** 속성을 설정의 값은 **고유한 스키마** 또는 **고유한 카탈로그** 속성 기본 테이블을 찾는 데 사용 됩니다. 알고리즘은 의도 한 있지만 필수는 해당 하나 또는 둘 다는 **고유한 스키마** 및 **고유한 카탈로그** 하기 전에 속성을 설정할 수는 **고유 테이블** 속성을 설정 합니다.  
  
 기본 키의 **고유 테이블** 전체의 기본 키로 처리 됩니다 **레코드 집합**합니다. 기본 키를 필요한 모든 메서드에 사용 되는 키입니다.  
  
 동안 **고유 테이블** 설정 되 면는 [삭제](../../../ado/reference/ado-api/delete-method-ado-recordset.md) 메서드 명명 된 테이블에만 영향을 줍니다. [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md), [Resync](../../../ado/reference/ado-api/resync-method.md), [업데이트](../../../ado/reference/ado-api/update-method.md), 및 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드가 모든 적절 한 기본 테이블의 의영향을**레코드 집합**합니다.  
  
 **고유 테이블** 재 모든 사용자 지정 동기화를 수행 하기 전에 지정 해야 합니다. 경우 **고유 테이블** 지정 되지 않은 [Resync Command](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md) 속성 아무런 효과가 없습니다.  
  
 고유한 기본 테이블을 찾을 수 없습니다 실행 시 오류가 발생 합니다.  
  
 이러한 동적 속성 모두에 추가 되는 **레코드 집합** 개체 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션 때는 [앞](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성이  **adUseClient**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
