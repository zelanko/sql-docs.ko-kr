---
title: "Seek 메서드 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset21::Seek
- Recordset21::raw_Seek
helpviewer_keywords: Seek method [ADO]
ms.assetid: 129293d2-19d3-4940-bf64-483ee72fb4a1
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8d94cf588916667e2cf82992b6a3ac6b601e8f84
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="seek-method"></a>Seek 메서드
인덱스를 검색 한 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 신속 하 게 지정된 된 값과 일치 하 고 해당 행에는 현재 행 위치를 변경 하는 행을 찾을 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.Seek KeyValues, SeekOption  
```  
  
#### <a name="parameters"></a>매개 변수  
 *KeyValues*  
 배열을 **Variant** 값입니다. 인덱스 하나 이상의 열으로 구성 하 고 배열에는 각 해당 열에 대해 비교할 값을 포함 합니다.  
  
 *SeekOption*  
 A [SeekEnum](../../../ado/reference/ado-api/seekenum.md) 인덱스의 열과 해당 간의 비교의 유형을 지정 하는 값 *KeyValues*합니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **Seek** 메서드와 함께 [인덱스](../../../ado/reference/ado-api/index-property.md) 기본 공급자에서 인덱스를 지 원하는 경우 속성은 **레코드 집합** 개체입니다. 사용 하 여는 [지원](../../../ado/reference/ado-api/supports-method.md)**(adSeek)** 기본 공급자에서 지원 하는지 여부를 확인할 수 있는 방법은 **Seek**, 및 **Supports(adIndex)** 공급자 인덱스를 지원 하는지 여부를 결정 하는 방법입니다. (예를 들어는 [OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) 지원 **Seek** 및 **인덱스**.)  
  
 경우 **Seek** 않습니다 찾을 원하는 행을 오류가 발생 하 고 행의 끝에 배치 되는 **레코드 집합**합니다. 설정의 **인덱스** 속성을이 메서드를 실행 하기 전에 원하는 인덱스입니다.  
  
 이 메서드는 서버 쪽 커서에만 지원 됩니다. 검색할 때 지원 되지 않습니다는 **레코드 집합** 개체의 [앞](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성 값은 **adUseClient**합니다.  
  
 이 메서드는 수만 있습니다 때 사용 되는 **레코드 집합** 개체도 연는 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 값 **adCmdTableDirect**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [메서드 및 속성 예제 (VB) 인덱스 검색](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [Seek 메서드 및 속성 예제 인덱스 (VC + +)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vc.md)   
 [Find 메서드 (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Index 속성](../../../ado/reference/ado-api/index-property.md)
