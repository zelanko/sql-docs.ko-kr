---
title: "AbsolutePage 속성 (ADO) | Microsoft Docs"
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
- Recordset15::AbsolutePage
helpviewer_keywords:
- AbsolutePage property [ADO]
ms.assetid: ddb58a35-ec3a-423c-a504-3c65e62c23d4
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 677b512a88fe3b6e695bd460cb0d4dea00ed673d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="absolutepage-property-ado"></a>AbsolutePage 속성 (ADO)
현재 레코드가 있는 페이지를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 32 비트 코드를 설정 하거나 반환는 **긴** 1에서에서 값의 페이지 수는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 ([PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)), 중 하나를 반환 하거나는 [PositionEnum ](../../../ado/reference/ado-api/positionenum.md) 값입니다.  
  
 64 비트 코드에 대 한 64 비트 값을 저장 하기 위해 제공 하는 데이터 형식을 사용 합니다. 하나를 사용할 수는 예를 들어 **긴** 또는 64 비트 길이 DBORDINAL 등 일 수 있는 다른 값입니다. 사용 하지 마십시오 **PositionEnum** 32 비트 길이 제한 되기 때문에 값입니다.  
  
## <a name="remarks"></a>주의  
 현재 레코드가 있는 페이지 수를 확인이 속성을 사용할 수 있습니다. 사용 하 여는 [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) 속성의 전체 행 집합 수를 논리적으로 분할 하는 **레코드 집합** 개체를 일련의 하며 각각의 같은 레코드 수가 페이지 **PageSize** (마지막 페이지를 제외 하 고 있는 있을 수 있습니다 더 적은 레코드). 공급자는이 속성을 사용할 수에 대 한 적절 한 기능을 지원 해야 합니다.  
  
-   가져오거나 설정할 때의 **AbsolutePage** 속성을 사용 하 여 ADO는 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) 속성 및 [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) 속성을 다음과 같이 함께:  
  
-   가져오려는 **AbsolutePage**, ADO가 먼저 검색는 **AbsolutePosition**, 다음으로 나눕니다는 **PageSize**합니다.  
  
-   설정 하는 **AbsolutePage**, ADO 이동은 **AbsolutePosition** 다음과 같이: 곱하는 것은 **PageSize** 새 **AbsolutePage** 값 한 후 값을 1을 추가 합니다. 현재 위치 하는 결과적으로 **레코드 집합** 성공적으로 설정한 후 **AbsolutePage** 는 해당 페이지에서 첫 번째 레코드입니다.  
  
 마찬가지로 **AbsolutePosition** 속성 **AbsolutePage** 는 1부터 시작 하 고 현재 레코드의 첫 번째 레코드는 경우는 **레코드 집합**합니다. 특정 페이지의 첫 번째 레코드로 이동 하려면이 속성을 설정 합니다. 페이지 합계를 구할는 **PageCount** 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [AbsolutePage, PageCount, 및 PageSize 속성 예제 (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage, PageCount, 및 PageSize 속성 예제 (VC + +)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePosition 속성 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 [PageCount 속성 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)   
 [PageSize 속성(ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)
