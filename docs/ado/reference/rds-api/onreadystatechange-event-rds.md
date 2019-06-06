---
title: onReadyStateChange 이벤트 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- onReadyStateChange event [ADO]
ms.assetid: bf2ae3ac-bfe4-4709-b50a-ea7c282c3164
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5fc38ed5f4c7fb7e2d12eaa1853b57eb0cdbc13a
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712558"
---
# <a name="onreadystatechange-event-rds"></a>onReadyStateChange 이벤트(RDS)
**onReadyStateChange** 이벤트 라고 때마다 값을 [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) 속성 변경 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
onReadyStateChange  
```  
  
#### <a name="parameters"></a>매개 변수  
 없음  
  
## <a name="remarks"></a>Remarks  
 합니다 **ReadyState** 의 진행 상황을 반영 하는 속성을 [rds. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체에 데이터를 비동기적으로 검색 하는 대로 해당 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다. 사용 하 여는 **onReadyStateChange** 의 변경 내용을 모니터링 하는 이벤트를 **ReadyState** 때마다 발생 하는 속성입니다. 이 속성의 값을 주기적으로 검사 보다 더 효율적입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>관련 항목  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)


