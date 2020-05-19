---
title: MaxRecords 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::MaxRecords
helpviewer_keywords:
- MaxRecords property [ADO]
ms.assetid: 20c76571-8c9a-482c-a99e-726ab1d93f8b
author: rothja
ms.author: jroth
ms.openlocfilehash: b9e4beaaa4b38a26089d1136d1b32090ea12231f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82754375"
---
# <a name="maxrecords-property-ado"></a>MaxRecords 속성(ADO)
쿼리에서 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 으로 반환할 최대 레코드 수를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 반환할 최대 레코드 수를 나타내는 **Long** 값을 설정 하거나 반환 합니다. 기본값은 영 (**0**)으로, 제한이 없음을 의미 합니다.  
  
## <a name="remarks"></a>설명  
 **MaxRecords** 속성을 사용 하 여 공급자가 데이터 원본에서 반환 하는 레코드 수를 제한할 수 있습니다. 이 속성의 기본 설정은 0 이며,이는 공급자가 요청 된 모든 레코드를 반환 함을 의미 합니다.  
  
 **MaxRecords** 속성은 **레코드 집합이** 닫혀 있을 때 읽기/쓰기이 고, 열려 있으면 읽기 전용입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [MaxRecords 속성 예제 (VB)](../../../ado/reference/ado-api/maxrecords-property-example-vb.md)   
 [MaxRecords 속성 예제(VC++)](../../../ado/reference/ado-api/maxrecords-property-example-vc.md)   
