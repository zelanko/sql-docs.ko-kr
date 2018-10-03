---
title: Fetchprogress 및 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FetchProgress
- Recordset::FetchProgress
helpviewer_keywords:
- FetchProgress event [ADO]
ms.assetid: 301716fd-81fc-40eb-8a04-221ef7ab410e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f47fb473d0120c124fd07fbb0b30bdecf991926f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47682165"
---
# <a name="fetchprogress-event-ado"></a>FetchProgress 및(ADO)
합니다 **FetchProgress**이벤트에 현재으로 가져온 보다 많은 행을 보고 하려면 시간이 오래 걸리는 비동기 작업을 하는 동안에 주기적으로 호출 됩니다 합니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
FetchProgress Progress, MaxProgress, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>매개 변수  
 *진행률*  
 A **긴** 인출 작업에서 현재 검색 된 레코드의 수를 나타내는 값입니다.  
  
 *MaxProgress*  
 A **긴** 검색할 레코드의 최대 수를 나타내는 값이 필요 합니다.  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) 상태 값입니다.  
  
 *pRecordset*  
 A **레코드 집합** 레코드는 검색 되는 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 사용 하는 경우 **FetchProgress** 자식이 있는 **레코드 집합**를 주의 하는 합니다 *진행률* 및 *MaxProgress* 매개 변수 값에서 파생 됩니다 기본 [커서 서비스](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) 행 집합입니다. 반환 되는 값에는 현재 챕터에 레코드의 수 뿐만 아니라 기본 행 집합의 레코드 총 수를 나타냅니다.  
  
> [!NOTE]
>  사용 하도록 **FetchProgress** with Microsoft Visual Basic, Visual Basic 6.0 이상가 필요 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)
