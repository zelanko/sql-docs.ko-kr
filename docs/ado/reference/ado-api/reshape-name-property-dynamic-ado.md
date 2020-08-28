---
description: Reshape Name 속성-동적(ADO)
title: 이름 변경 속성-동적 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Reshape Name property [ADO]
ms.assetid: 690229d1-46cc-42e6-a57d-4438251fe248
author: rothja
ms.author: jroth
ms.openlocfilehash: dbffa574fd9746788c38b6c03d9690a91ff89730
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989544"
---
# <a name="reshape-name-property-dynamic-ado"></a>Reshape Name 속성-동적(ADO)
[레코드 집합](./recordset-object-ado.md) 개체의 이름을 지정 합니다.  
  
## <a name="return-values"></a>반환 값  
 **레코드 집합**의 이름인 **문자열** 값을 반환 합니다.  
  
## <a name="remarks"></a>설명  
 이름은 연결 기간 동안 또는 **레코드 집합** 을 닫을 때까지 유지 됩니다.  
  
 **이름 변경** 속성은 주로 OLE DB 서비스 공급자 [용 Microsoft 데이터 셰이핑 서비스](../../guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) 의 재구성 기능에서 사용 하기 위한 것입니다. 다시 셰이핑에 참여 하려면 이름이 고유 해야 합니다.  
  
 이 속성은 읽기 전용 이지만 **레코드 집합** 을 만들 때 간접적으로 설정할 수 있습니다. 예를 들어 Shape 명령의 절에서 **레코드 집합** 을 만들고 **AS** 키워드를 사용 하 여 별칭 이름을 지정 하는 경우 별칭은 **이름 변경** 속성에 할당 됩니다. 별칭이 선언 되지 않은 경우 **이름 변경** 속성에는 데이터 셰이핑 서비스에 의해 생성 된 고유 이름이 할당 됩니다. 별칭 이름이 기존 **레코드 집합**의 이름과 같을 경우 둘 중 하나를 해제할 때까지 **레코드 집합** 을 변경할 수 없습니다. ADO 연결에서 [이름 변경]() 속성의 고유한 이름을 **True**로 설정 하 여 기본 동작을 변경할 수 있습니다. 이 속성을 설정 하면 필요한 경우 사용자가 지정한 이름을 변경 하 여 고유성이 보장 되는 데이터 셰이핑 서비스 권한이 제공 됩니다. 모양 변경에 대 한 자세한 내용은 [OLE DB Microsoft 데이터 셰이핑 서비스 (ADO 서비스 공급자)](../../guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)를 참조 하세요.  
  
 셰이프 명령에서 **레코드 집합** 을 참조 하려는 경우 또는 데이터 셰이핑 서비스에서 생성 되었기 때문에 이름을 알 수 없는 경우에는 **이름 변경** 속성을 사용 합니다. 이 경우 **이름 변경** 속성에 의해 반환 되는 문자열 주위에 명령을 연결 하 여 SHAPE 명령을 생성할 수 있습니다.  
  
 [CursorLocation](./cursorlocation-property-ado.md) 속성이 **adUseClient**로 설정 된 경우, **이름 변경** 은 **레코드 집합** 개체의 [Properties](./properties-collection-ado.md) 컬렉션에 추가 되는 동적 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [OLE DB 용 Microsoft 데이터 셰이핑 서비스 (ADO 서비스 공급자)](../../guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)   
 [Shape 명령 일반](../../guide/data/shape-commands-in-general.md)   
 [레코드 집합 개체(ADO)](./recordset-object-ado.md)