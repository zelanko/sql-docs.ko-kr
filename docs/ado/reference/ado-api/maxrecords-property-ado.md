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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac5097a8692ed7a9e6566707354112547c5a619c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62864014"
---
# <a name="maxrecords-property-ado"></a>MaxRecords 속성(ADO)
반환할 레코드의 최대 수를 나타내는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 쿼리에서 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환 된 **긴** 반환할 레코드의 최대 수를 나타내는 값입니다. 기본값은 0 (**0**), 제한이 없음을 의미 합니다.  
  
## <a name="remarks"></a>Remarks  
 사용 된 **MaxRecords** 공급자 데이터 원본에서 반환 하는 레코드의 수를 제한 하는 속성입니다. 이 속성의 기본값은 레코드를 요청 된 모든 공급자가 반환 됨을 나타내는 0입니다.  
  
 **MaxRecords** 속성은 읽기/쓰기 경우 합니다 **레코드 집합** 열려 있는 경우에 닫힌 이며 읽기 전용입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [MaxRecords 속성 예제 (VB)](../../../ado/reference/ado-api/maxrecords-property-example-vb.md)   
 [MaxRecords 속성 예제(VC++)](../../../ado/reference/ado-api/maxrecords-property-example-vc.md)   
