---
title: "MaxRecords 속성 (ADO) | Microsoft Docs"
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
- Recordset15::MaxRecords
helpviewer_keywords:
- MaxRecords property [ADO]
ms.assetid: 20c76571-8c9a-482c-a99e-726ab1d93f8b
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7d6991928fdf3c284f7039b75f96a95fd93e0be3
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="maxrecords-property-ado"></a>MaxRecords 속성 (ADO)
반환 하는 레코드의 최대 수를 나타내는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 쿼리에서 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **긴** 반환할 레코드의 최대 수를 나타내는 값입니다. 기본값은 0 (**0**), 제한이 없음을 의미 합니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **MaxRecords** 공급자 데이터 원본에서 반환 하는 레코드의 수를 제한 하는 속성입니다. 이 속성의 기본 설정은 0 이며 공급자에서 반환 하는 요청 된 모든 레코드를입니다.  
  
 **MaxRecords** 속성은 읽기/쓰기 때는 **레코드 집합** 열려 있는 경우에 닫힌 이며 읽기 전용입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [MaxRecords 속성 예제 (VB)](../../../ado/reference/ado-api/maxrecords-property-example-vb.md)   
 [MaxRecords 속성 예제(VC++)](../../../ado/reference/ado-api/maxrecords-property-example-vc.md)   
