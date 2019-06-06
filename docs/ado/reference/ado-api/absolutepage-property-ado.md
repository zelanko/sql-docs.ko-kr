---
title: AbsolutePage 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AbsolutePage
helpviewer_keywords:
- AbsolutePage property [ADO]
ms.assetid: ddb58a35-ec3a-423c-a504-3c65e62c23d4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c87862f97a1fc00d625542c177d85e11d0a7ad45
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66699278"
---
# <a name="absolutepage-property-ado"></a>AbsolutePage 속성(ADO)
현재 레코드가 있는 페이지를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 32 비트 코드를 설정 하거나 반환을 **긴** 의 페이지 수가 1에서 값을 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 ([PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)), 중 하나를 반환 하거나는 [PositionEnum ](../../../ado/reference/ado-api/positionenum.md) 값입니다.  
  
 64 비트 코드를 64 비트 값의 저장소를 제공 하는 데이터 형식을 사용 합니다. 예를 들어 사용할 수 있습니다 **긴** 또는 다른 값 DBORDINAL와 같은 64 비트 길이 수 있습니다. 사용 하지 마세요 **PositionEnum** 32 비트 길이 제한 되므로 값입니다.  
  
## <a name="remarks"></a>Remarks  
 현재 레코드에 있는 페이지 수를 확인 하려면이 속성을 사용할 수 있습니다. 사용 하 여는 [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) 속성의 전체 행 집합 수를 논리적으로 분할 하는 **레코드 집합** 일련의 페이지에는 각각의 같은 레코드 수가 개체로 **PageSize** (마지막 페이지를 제외 하 고는 할 수도 더 적은 레코드). 공급자 사용 가능 하도록이 속성에 대 한 적절 한 기능을 지원 해야 합니다.  
  
-   가져오거나 설정 합니다 **AbsolutePage** 속성을 사용 하 여 ADO 합니다 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) 속성 및 [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) 속성을 다음과 같이 함께:  
  
-   가져올는 **AbsolutePage**, ADO를 먼저 검색를 **AbsolutePosition**, 다음으로 나눕니다를 **PageSize**합니다.  
  
-   설정 하는 **AbsolutePage**, ADO 이동 합니다 **AbsolutePosition** 같이: 곱하여를 **PageSize** 새 **AbsolutePage** 값 및 다음 값에 1을 추가 합니다. 현재 위치 하는 결과적으로 **레코드 집합** 설정이 완료 된 후 **AbsolutePage** 해당 페이지의 첫 번째 레코드는 합니다.  
  
 같은 합니다 **AbsolutePosition** 속성인 **AbsolutePage** 는 1부터 시작 하 고 현재 레코드에서 첫 번째 레코드는 1이를 **레코드 집합**. 특정 페이지의 첫 번째 레코드를 이동 하려면이 속성을 설정 합니다. 페이지 합계를 구할 합니다 **PageCount** 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [AbsolutePage, PageCount, PageSize 속성 예제 (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage, PageCount, PageSize 속성 예제 (VC + +)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePosition 속성 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 [PageCount 속성 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)   
 [PageSize 속성(ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)
