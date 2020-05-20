---
title: Open 메서드 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Open
- Cellset::Open
helpviewer_keywords:
- Open method [ADO MD]
ms.assetid: a87d8080-a238-45e5-bc80-9a8625b3810f
author: rothja
ms.author: jroth
ms.openlocfilehash: c0469bef1bce402efe143fbaa1ac760e3465d630
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765118"
---
# <a name="open-method-ado-md"></a>Open 메서드(ADO MD)
다차원 쿼리 결과를 검색 하 고 결과를 [셀 집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)에 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Cellset.Open Source, ActiveConnection  
```  
  
#### <a name="parameters"></a>매개 변수  
 *소스*  
 (선택 사항) MDX (Multidimensional Expression) 쿼리와 같은 유효한 다차원 쿼리로 계산 되는 **Variant** 입니다. *Source* 인수는 [source](../../../ado/reference/ado-md-api/source-property-ado-md.md) 속성에 해당 합니다. MDX에 대 한 자세한 내용은 Microsoft Data Access Components SDK의 [OLAP (온라인 분석 처리)](https://msdn.microsoft.com/8a7673c6-3ca1-4411-9f1e-adf1e47df4f3) 설명서에 대 한 OLE DB를 참조 하세요.  
  
 *ActiveConnection*  
 (선택 사항) 유효한 ADO [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 변수 이름 또는 연결에 대 한 정의를 지정 하는 문자열로 계산 되는 **Variant** 입니다. *ActiveConnection* 인수는 [셀 집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 개체를 열 연결을 지정 합니다. 이 인수에 대 한 연결 정의를 전달 하면 ADO에서 지정 된 매개 변수를 사용 하 여 새 연결을 엽니다. *ActiveConnection* 인수는 [ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md) 속성에 해당 합니다.  
  
## <a name="remarks"></a>설명  
 **Open** 메서드는 매개 변수 중 하나를 생략 하 고 해당 속성 값이 설정 되지 않은 경우 **셀**집합을 열려고 하기 전에 오류를 생성 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Cellset 개체(ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>참고 항목  
 [셀 집합 예제 (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [ActiveConnection 속성 (ADO MD)](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md)   
 [Close 메서드 (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Connection 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Source 속성 (ADO MD)](../../../ado/reference/ado-md-api/source-property-ado-md.md)   
 [State 속성(ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
