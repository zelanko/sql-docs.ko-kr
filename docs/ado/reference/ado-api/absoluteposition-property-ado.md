---
title: AbsolutePosition 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AbsolutePosition
helpviewer_keywords:
- AbsolutePosition property [ADO]
ms.assetid: 79f8ee5e-fc70-46d8-8c29-ebf943c66592
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 467834d2cfd5e56c14d9c7565d6749fa6848251e
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718352"
---
# <a name="absoluteposition-property-ado"></a>AbsolutePosition 속성(ADO)
서 수 위치를 나타내는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체의 현재 레코드입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 32 비트 코드를 설정 하거나 반환을 **긴** 레코드의 수가 1에서 값을 **레코드 집합** 개체 ([RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)), 중 하나를 반환 하거나는 [ PositionEnum](../../../ado/reference/ado-api/positionenum.md) 값입니다.  
  
 64 비트 코드를 64 비트 값의 저장소를 제공 하는 데이터 형식을 사용 합니다. 예를 들어, Long 또는 다른을 사용할 수 있습니다 DBORDINAL와 같은 64 비트 길이 값입니다. 사용 하지 마세요 **PositionEnum** 32 비트 길이 제한 되므로 값입니다.  
  
## <a name="remarks"></a>Remarks  
 설정 하기 위해 합니다 **AbsolutePosition** 속성, ADO를 사용 하는 OLE DB 공급자를 구현 해야 합니다 [IRowsetLocate:IRowset](https://msdn.microsoft.com/library/windows/desktop/ms721190.aspx) 인터페이스입니다.  
  
 에 액세스 하는 **AbsolutePosition** 의 속성을 **레코드 집합** 정방향 전용 중 하나를 사용 하 여 열려 있는 하거나 동적 커서에 오류를 발생 시킵니다 **adErrFeatureNotAvailable**. 기타 커서 유형으로 올바른 위치 반환할 OLE DB 공급자를 지원 하기만 합니다 **IRowsetScroll:IRowsetLocate** 인터페이스입니다. 공급자를 지원 하지 않는 경우는 **IRowsetScroll** 인터페이스의 속성이로 설정 되어 **adPosUnknown**합니다. 지원 하는지 여부를 확인 하 여 공급자에 대 한 설명서를 참조 하세요 **IRowsetScroll**합니다.  
  
 사용 하 여는 **AbsolutePosition** 레코드로 이동할 속성의 서 수 위치에 따라는 **레코드 집합** 개체 또는 현재 레코드의 서 수 위치를 결정 합니다. 공급자 사용 가능 하도록이 속성에 대 한 적절 한 기능을 지원 해야 합니다.  
  
 같은 합니다 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) 속성인 **AbsolutePosition** 는 1부터 시작 하 고 현재 레코드에서 첫 번째 레코드는 1이를 **레코드 집합**. 레코드의 총 수를 가져올 수 있습니다는 **Recordset** 에서 개체를 [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) 속성.  
  
 설정한 경우 합니다 **AbsolutePosition** 속성인 경우에 현재 캐시에서 레코드를 ADO 캐시를 다시 로드 하면 지정 된 레코드를 사용 하 여 시작 하는 레코드의 새 그룹을 사용 하 여 합니다. 합니다 [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) 속성이이 그룹의 크기를 결정 합니다.  
  
> [!NOTE]
>  사용 하지 않아야 합니다 **AbsolutePosition** 서로게이트 레코드 숫자로 속성입니다. 지정된 된 레코드의 위치는 이전 레코드를 삭제 하는 경우 변경 됩니다. 지정된 된 레코드 같은 가질 수 없습니다 assurance 이기도 **AbsolutePosition** 경우는 **레코드 집합** 개체 다시 쿼리되어 되었거나 다시 합니다. 책갈피는 계속 유지 하 고 지정된 된 위치를 반환 하는 권장된 방법을 이며 모든 형식의 위치 통해서만 **레코드 집합** 개체입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [AbsolutePosition 및 CursorLocation 속성 예제 (VB)](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vb.md)   
 [AbsolutePosition 및 CursorLocation 속성 예제 (VC + +)](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vc.md)   
 [AbsolutePage 속성 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [RecordCount 속성(ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
