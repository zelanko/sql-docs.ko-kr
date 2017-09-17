---
title: "AbsolutePosition 속성 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::AbsolutePosition
helpviewer_keywords:
- AbsolutePosition property [ADO]
ms.assetid: 79f8ee5e-fc70-46d8-8c29-ebf943c66592
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9c8a31bd7b0fbf2809b09b10b2ebcb983d7c811c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="absoluteposition-property-ado"></a>AbsolutePosition 속성 (ADO)
서 수 위치를 나타내며는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체의 현재 레코드입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 32 비트 코드를 설정 하거나 반환는 **긴** 1에서에서 값의 레코드 수는 **레코드 집합** 개체 ([RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)), 중 하나를 반환 하거나는 [ PositionEnum](../../../ado/reference/ado-api/positionenum.md) 값입니다.  
  
 64 비트 코드에 대 한 64 비트 값을 저장 하기 위해 제공 하는 데이터 형식을 사용 합니다. 예를 들어 Long 또는 다른를 사용할 수 있습니다 DBORDINAL와 같은 64 비트 길이 값입니다. 사용 하지 마십시오 **PositionEnum** 값을 32 비트 길이 제한 되기 때문입니다.  
  
## <a name="remarks"></a>주의  
 설정 하는 데는 **AbsolutePosition** 속성, ADO 필요를 사용 하는 OLE DB 공급자를 구현 하는 [IRowsetLocate:IRowset](https://msdn.microsoft.com/library/windows/desktop/ms721190.aspx) 인터페이스입니다.  
  
 에 액세스 하는 **AbsolutePosition** 속성의는 **레코드 집합** 정방향 전용 사용 하 여 열린 된 동적 커서에는 오류를 발생 시킵니다. 또는 **adErrFeatureNotAvailable**합니다. 다른 커서 유형으로 올바른 위치 반환할으로 지 원하는 OLE DB 공급자는 **IRowsetScroll:IRowsetLocate** 인터페이스입니다. 공급자를 지원 하지 않는 경우는 **IRowsetScroll** 인터페이스의 속성이로 설정 되어 **adPosUnknown**합니다. 지원 하는지 여부를 확인 하 여 공급자에 대 한 설명서를 참조 **IRowsetScroll**합니다.  
  
 사용 하 여는 **AbsolutePosition** 레코드로 이동 하는 속성의 서 수 위치에 따라는 **레코드 집합** 개체 또는 현재 레코드의 서 수 위치를 결정 합니다. 공급자는이 속성을 사용할 수에 대 한 적절 한 기능을 지원 해야 합니다.  
  
 마찬가지로 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) 속성 **AbsolutePosition** 는 1부터 시작 하 고 현재 레코드의 첫 번째 레코드는 경우는 **레코드 집합**합니다. 에 있는 레코드의 총 수를 가져올 수 있습니다는 **레코드 집합** 에서 개체는 [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) 속성입니다.  
  
 설정 하는 경우는 **AbsolutePosition** 속성, 현재 캐시에서 레코드를가 하는 경우에 ADO 캐시를 다시 로드와 지정한 레코드부터 시작 하는 레코드의 새로운 그룹입니다. [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) 속성이이 그룹의 크기를 결정 합니다.  
  
> [!NOTE]
>  사용 하지 않아야는 **AbsolutePosition** 속성으로 서로게이트 레코드 번호입니다. 지정된 된 레코드의 위치는 이전 레코드를 삭제 하는 경우 변경 됩니다. 지정된 된 레코드 같은 가질 수 없는 보증 이기도 **AbsolutePosition** 경우는 **레코드 집합** 개체가 쿼리가 다시 실행 또는 다시 열입니다. 책갈피는 계속 유지 하 고 지정된 된 위치를 반환 하는 권장된 방법 및 모든 종류의에서 위치를 지정 하는 유일한 방법은 **레코드 집합** 개체입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [AbsolutePosition 및 앞 속성 예제 (VB)](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vb.md)   
 [AbsolutePosition 및 앞 속성 예제 (VC + +)](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vc.md)   
 [AbsolutePage 속성 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [RecordCount 속성(ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)

