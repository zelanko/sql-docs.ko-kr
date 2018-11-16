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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 091073431b3ff349b8ae107fcb6a37bfab94e46e
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51602783"
---
# <a name="open-method-ado-md"></a>Open 메서드(ADO MD)
다차원 쿼리 결과 검색 하 고 결과를 반환 된 [셀 집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Cellset.Open Source, ActiveConnection  
```  
  
#### <a name="parameters"></a>매개 변수  
 *원본*  
 선택 사항입니다. A **Variant** MDX (Multidimensional Expression) 쿼리 등 유효한 다차원 쿼리를 계산 합니다. 합니다 *소스* 인수에 해당 합니다 [원본](../../../ado/reference/ado-md-api/source-property-ado-md.md) 속성입니다. MDX에 대 한 자세한 내용은 참조는 [OLE DB에 대 한 분석 처리 OLAP (온라인)](https://msdn.microsoft.com/8a7673c6-3ca1-4411-9f1e-adf1e47df4f3) Microsoft Data Access Components SDK 설명서.  
  
 *ActiveConnection*  
 선택 사항입니다. A **Variant** 로 평가 되는 중 하나를 지정 하는 문자열을 유효한 ADO [연결](../../../ado/reference/ado-api/connection-object-ado.md) 변수 이름 또는 연결에 대 한 정의 개체입니다. 합니다 *ActiveConnection* 인수를 열 때 사용할 연결을 지정 합니다 [셀 집합](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) 개체입니다. 이 인수에 대 한 연결 정의 전달 하는 경우 ADO는 지정된 된 매개 변수를 사용 하 여 새 연결을 엽니다. 합니다 *ActiveConnection* 인수에 해당 합니다 [ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md) 속성입니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 **엽니다** 메서드는 해당 매개 변수 중 하나가 생략 되 고 열기를 시도 하기 전에 해당 속성 값 설정 되지 않은 경우 오류를 생성 합니다 **셀 집합**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Cellset 개체(ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>관련 항목  
 [Cellset 예제 (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [ActiveConnection 속성 (ADO MD)](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md)   
 [Close 메서드 (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Source 속성 (ADO MD)](../../../ado/reference/ado-md-api/source-property-ado-md.md)   
 [State 속성(ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
