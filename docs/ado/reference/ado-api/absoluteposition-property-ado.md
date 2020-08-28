---
description: AbsolutePosition 속성(ADO)
title: AbsolutePosition 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0ecb3290d73032568af7e0a92baf0c9d1b2628f4
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977163"
---
# <a name="absoluteposition-property-ado"></a>AbsolutePosition 속성(ADO)
[레코드 집합](./recordset-object-ado.md) 개체의 현재 레코드의 서 수 위치를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 32 비트 코드의 경우 1에서 레코드 **집합** 개체 ([RecordCount](./recordcount-property-ado.md))의 레코드 수 까지의 **Long** 값을 설정 또는 반환 하거나 [positionenum](./positionenum.md) 값 중 하나를 반환 합니다.  
  
 64 비트 코드의 경우 64 비트 값의 저장소에 대해 제공 하는 데이터 형식을 사용 합니다. 예를 들어, Long 또는 DBORDINAL과 같은 64 비트 길이의 다른 값을 사용할 수 있습니다. **Positionenum** 값은 32 비트 길이로 제한 되므로 사용 하지 마십시오.  
  
## <a name="remarks"></a>설명  
 ADO에서는 **AbsolutePosition** 속성을 설정 하기 위해 사용 하는 OLE DB 공급자가 [IRowsetLocate: IRowset](/previous-versions/windows/desktop/ms721190(v=vs.85)) 인터페이스를 구현 해야 합니다.  
  
 앞 으로만 이동 하거나 동적 커서를 사용 하 여 연 **레코드 집합** 의 **AbsolutePosition** 속성에 액세스 하면 **adErrFeatureNotAvailable**오류가 발생 합니다. 다른 커서 유형을 사용 하는 경우 OLE DB 공급자가 **IRowsetScroll: IRowsetLocate** 인터페이스를 지원 하기만 하면 올바른 위치가 반환 됩니다. 공급자가 **IRowsetScroll** 인터페이스를 지원 하지 않는 경우 속성은 **adPosUnknown**로 설정 됩니다. **IRowsetScroll**을 지원 하는지 여부를 확인 하려면 공급자에 대 한 설명서를 참조 하세요.  
  
 **AbsolutePosition** 속성을 사용 하 여 레코드 **집합** 개체의 서 수 위치에 따라 레코드를 이동 하거나 현재 레코드의 서 수 위치를 확인 합니다. 공급자는이 속성을 사용할 수 있는 적절 한 기능을 지원 해야 합니다.  
  
 [AbsolutePage](./absolutepage-property-ado.md) 속성 처럼 **AbsolutePosition** 은 1부터 시작 하 고 현재 레코드가 **레코드 집합**의 첫 번째 레코드인 경우 1과 같습니다. [RecordCount](./recordcount-property-ado.md) 속성에서 레코드 **집합** 개체의 총 레코드 수를 가져올 수 있습니다.  
  
 **AbsolutePosition** 속성을 설정 하는 경우 현재 캐시의 레코드를 사용 하는 경우에도 ADO는 지정 된 레코드부터 시작 하 여 새 레코드 그룹을 사용 하 여 캐시를 다시 로드 합니다. [CacheSize](./cachesize-property-ado.md) 속성은이 그룹의 크기를 결정 합니다.  
  
> [!NOTE]
>  **AbsolutePosition** 속성은 서로게이트 레코드 번호로 사용 하면 안 됩니다. 이전 레코드를 삭제 하면 지정 된 레코드의 위치가 변경 됩니다. 또한 **레코드 집합** 개체를 다시 만들거나 다시 열 경우 지정 된 레코드가 동일한 **AbsolutePosition** 를 갖게 됩니다. 책갈피는 지정 된 위치를 유지 하 고 반환 하는 데 권장 되는 방법 이지만 모든 형식의 **레코드 집합** 개체에서 위치를 지정 하는 유일한 방법입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [AbsolutePosition 및 CursorLocation 속성 예제 (VB)](./absoluteposition-and-cursorlocation-properties-example-vb.md)   
 [AbsolutePosition 및 CursorLocation 속성 예제 (VC + +)](./absoluteposition-and-cursorlocation-properties-example-vc.md)   
 [AbsolutePage 속성 (ADO)](./absolutepage-property-ado.md)   
 [RecordCount 속성(ADO)](./recordcount-property-ado.md)