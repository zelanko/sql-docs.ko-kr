---
description: Seek 메서드
title: Seek 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset21::Seek
- Recordset21::raw_Seek
helpviewer_keywords:
- Seek method [ADO]
ms.assetid: 129293d2-19d3-4940-bf64-483ee72fb4a1
author: rothja
ms.author: jroth
ms.openlocfilehash: 3325cbb2a1178be61167cc0291bf23564d1e84fb
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777522"
---
# <a name="seek-method"></a>Seek 메서드
[레코드 집합](./recordset-object-ado.md) 의 인덱스를 검색 하 여 지정 된 값과 일치 하는 행을 빠르게 찾고 현재 행 위치를 해당 행으로 변경 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.Seek KeyValues, SeekOption  
```  
  
#### <a name="parameters"></a>매개 변수  
 *KeyValues*  
 **변형** 값의 배열입니다. 인덱스는 하나 이상의 열로 구성 되며 배열에는 해당 하는 각 열에 대해 비교할 값이 포함 됩니다.  
  
 *SeekOption*  
 인덱스의 열과 해당 하는 *Keyvalues*사이에서 수행할 비교 유형을 지정 하는 [SeekEnum](./seekenum.md) 값입니다.  
  
## <a name="remarks"></a>설명  
 기본 공급자가 **레코드 집합** 개체에 대 한 인덱스를 지 원하는 경우에는 [Index](./index-property.md) 속성과 함께 **Seek** 메서드를 사용 합니다. [지원](./supports-method.md)**(adseek)** 메서드를 사용 하 여 기본 공급자가 **Seek**를 지원 하는지 여부를 확인 하 고 **지원 (adseek)** 메서드를 사용 하 여 공급자가 인덱스를 지원 하는지 여부를 확인 합니다. 예를 들어 [Microsoft Jet 용 OLE DB 공급자](../../guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) 는 **검색** 및 **인덱스**를 지원 합니다.  
  
 **검색** 에서 원하는 행을 찾지 못하면 오류가 발생 하지 않으며 **레코드 집합**의 끝에 행이 배치 됩니다. 이 메서드를 실행 하기 전에 **인덱스** 속성을 원하는 인덱스로 설정 합니다.  
  
 이 메서드는 서버 쪽 커서 에서만 지원 됩니다. **레코드 집합** 개체의 [CursorLocation](./cursorlocation-property-ado.md) 속성 값이 **adUseClient**인 경우 검색은 지원 되지 않습니다.  
  
 이 메서드는 [CommandTypeEnum](./commandtypeenum.md) 값 **adCmdTableDirect**를 사용 하 여 **레코드 집합** 개체를 연 경우에만 사용할 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Seek 메서드 및 인덱스 속성 예제 (VB)](./seek-method-and-index-property-example-vb.md)   
 [Seek 메서드 및 인덱스 속성 예제 (VC + +)](./seek-method-and-index-property-example-vc.md)   
 [Find 메서드 (ADO)](./find-method-ado.md)   
 [Index 속성](./index-property.md)