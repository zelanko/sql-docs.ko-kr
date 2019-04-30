---
title: Reshape Name 속성-동적 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Reshape Name property [ADO]
ms.assetid: 690229d1-46cc-42e6-a57d-4438251fe248
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6a07ec878b1198fbf23bfb251460d83869313c83
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63062131"
---
# <a name="reshape-name-property-dynamic-ado"></a>Reshape Name 속성-동적(ADO)
이름을 지정 합니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
## <a name="return-values"></a>반환 값  
 반환 된 **문자열** 값의 이름입니다 합니다 **레코드 집합**합니다.  
  
## <a name="remarks"></a>Remarks  
 때까지 또는 연결의 기간에 대 한 이름을 유지 합니다 **레코드 집합** 닫혀 있습니다.  
  
 **변형 이름** 속성은 주로의 다시 셰이핑 기능을 사용 하 여 사용 합니다 [OLE DB에 대 한 Microsoft Data Shaping Service](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) 서비스 공급자입니다. 이름은 다시 형성에 참여 하도록 고유 해야 합니다.  
  
 이 속성은 읽기 전용 이지만 설정할 수 있습니다 하지 직접 경우는 **레코드 집합** 만들어집니다. 예를 들어 경우 절에는 Shape 명령을 만듭니다는 **레코드 집합** 를 사용 하 여 별칭 이름을 제공 합니다 **AS** 키워드 별칭에 할당 된를 **변형 이름** 속성. 별칭 없음로 선언 된 경우는 **변형 이름** 속성 데이터 셰이핑 서비스에서 생성 된 고유한 이름이 할당 됩니다. 별칭 이름이 기존 이름과 동일 **Recordset**되지 않습니다 **Recordset** 둘 중 해제 될 때까지 모양을 변경할 수 있습니다. 고유 이름을 설정 하 여 기본 동작을 변경할 수 있습니다는 [이름은 변형](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md) 속성에 대 한 ADO 연결을 **True**. 데이터 셰이핑 고유성을 보장 하는 데 필요한 경우 할당 된 사용자 이름을 변경 하려면 서비스 사용 권한 제공이 속성을 설정 합니다. 모양 변경 하는 방법에 대 한 자세한 내용은 참조 하세요. [OLE DB (ADO 서비스 공급자)에 대 한 Microsoft Data Shaping Service](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)합니다.  
  
 사용 하 여는 **변형 이름** 참조 하려는 경우 속성을 **레코드 집합** 셰이프 명령 또는 데이터 셰이핑 서비스에서 생성 되어 있으므로 이름을 모를 경우. 이때 명령에서 반환한 문자열 주위에 연결 하 여 SHAPE 명령을 생성할 수 있습니다 합니다 **변형 이름** 속성입니다.  
  
 **이름 변형** 에 추가 하는 동적 속성을 **레코드 집합** 개체의 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션 때 합니다 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성**adUseClient**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft 데이터 셰이핑 OLE DB (ADO 서비스 공급자)에 대 한 서비스](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
