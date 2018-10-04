---
title: 컨트롤 (ADO) 레코드 집합 기본 테이블에 변경 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bcca3701807ebb591a0c083c4f4762b7597b9856
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47777391"
---
# <a name="unique-table-unique-schema-unique-catalog-properties-dynamic-ado"></a>고유 테이블, 고유 스키마, 고유 카탈로그 속성-동적 (ADO)
특정 기본 테이블에 밀접 하 게 제어 수정 하면를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 여러 기본 테이블에서 조인 작업을 하 여 형성 하는 합니다.  
  
-   **고유 테이블** 기반이 업데이트, 삽입 및 삭제를 수행할 기본 테이블의 이름을 지정 합니다.  
  
-   **고유한 스키마** 지정 된 *스키마*, 또는 테이블의 소유자 이름입니다.  
  
-   **고유 카탈로그** 지정 된 *카탈로그*, 또는 테이블이 포함 된 데이터베이스의 이름입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환 된 **문자열** 값 테이블, 스키마 또는 카탈로그의 이름입니다.  
  
## <a name="remarks"></a>Remarks  
 원하는 기본 테이블에는 해당 카탈로그, 스키마 및 테이블 이름으로 고유 하 게 식별 됩니다. 경우는 **고유 테이블** 속성을 설정의 값을 **고유한 스키마** 또는 **고유 카탈로그** 속성은 기본 테이블을 찾는 데. 의도 한 것 이지만 필수는 하나 또는 둘 다를 **고유한 스키마** 및 **고유 카탈로그** 하기 전에 속성을 설정할 수는 **고유 테이블** 속성을 설정 합니다.  
  
 기본 키를 **고유 테이블** 전체의 기본 키로 처리 됩니다 **Recordset**합니다. 기본 키에 필요한 모든 메서드에 사용 되는 키입니다.  
  
 하는 동안 **고유 테이블** 으로 설정 합니다 [삭제](../../../ado/reference/ado-api/delete-method-ado-recordset.md) 메서드 명명된 된 테이블에 영향을 줍니다. [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md), [Resync](../../../ado/reference/ado-api/resync-method.md)를 [업데이트](../../../ado/reference/ado-api/update-method.md), 및 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드가 는모든적절한기본기본테이블에영향을**레코드 집합**합니다.  
  
 **고유 테이블** 모든 사용자 지정 재 동기화를 수행 하기 전에 지정 해야 합니다. 하는 경우 **고유 테이블** 지정 하지는 [Resync Command](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md) 속성 영향을 주지 것입니다.  
  
 런타임 오류에는 고유한 기본 테이블을 찾을 수 없는 경우 발생 합니다.  
  
 이러한 동적 속성에 추가 됩니다 모든는 **레코드 집합** 개체 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션 때를 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성이  **adUseClient**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
