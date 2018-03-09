---
title: "RecordCount 속성 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::RecordCount
- Recordset15::GetRecordCount
- Recordset15::get_RecordCount
helpviewer_keywords:
- RecordCount property [ADO]
ms.assetid: 834f0121-394a-44d4-ad7d-999b43a6fe63
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 92faeb5d2ec0b62c03292f71e0299c779e362478
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="recordcount-property-ado"></a>RecordCount 속성 (ADO)
에 있는 레코드의 수를 나타내는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 반환 된 **긴** 의 레코드 수를 나타내는 값은 **레코드 집합**합니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **RecordCount** 속성을 레코드에 있는 한 **레코드 집합** 개체입니다. 속성 공급자 또는 커서 유형을 지원 하지 않는 경우 또는 ADO 레코드의 수를 확인할 수 없는 경우-1을 반환 **RecordCount**합니다. 읽기는 **RecordCount** 닫힌된 속성 **레코드 집합** 하면 오류가 발생 합니다.  
  
 경우는 **레코드 집합** 개체 대략적인 위치를 지원 또는 책갈피??? 즉, **지원 (adApproxPosition)** 또는 **지원 (adBookmark)**각각 반환 **True**??? 이 값에 있는 레코드의 정확한 수 있게 됩니다는 **레코드 집합**여부 완전히 채워진에 관계 없이 합니다. 경우는 **레코드 집합** 개체가 대략적인 위치를 지원 하지 않습니다, 모든 레코드를 검색 하 고 정확한 반환할 계산 때문에이 속성 리소스가 많이 소모 못할 **RecordCount** 값입니다.  
  
> [!NOTE]
>  ADO 2.8 및 이전 버전에서는 SQLOLEDB 공급자를 인출 모든 레코드를 반환 하는 경우에도 서버 쪽 커서를 사용 하면 **True** 둘 다에 대해 **지원 (adApproxPosition)** 및 **지원 (adBookmark)**합니다.  
  
 커서 유형의 **레코드 집합** 개체 레코드의 수를 확인할 수 있는지 여부에 영향을 줍니다. **RecordCount** 속성은 데이터 원본에 따라 동적 커서에 대 한 실제 개수 또는-1을 정방향 전용 커서, 정적 실제 개수 또는 키 집합 커서; 및-1을 반환 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [필터 및 RecordCount 속성 예제 (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
 [필터 및 RecordCount 속성 예제 (VC + +)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
 [AbsolutePosition 속성 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 [PageCount 속성(ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
