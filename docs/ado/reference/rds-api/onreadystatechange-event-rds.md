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
author: rothja
ms.author: jroth
ms.openlocfilehash: 00eb7b7084506de78262f4df2a4606c6756bbacb
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82751446"
---
# <a name="onreadystatechange-event-rds"></a>onReadyStateChange 이벤트(RDS)
**OnReadyStateChange** 이벤트는 [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) 속성 값이 변경 될 때마다 호출 됩니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
onReadyStateChange  
```  
  
#### <a name="parameters"></a>매개 변수  
 없음  
  
## <a name="remarks"></a>설명  
 **ReadyState** 속성은 RDS의 진행 상황을 반영 합니다 [. ](../../../ado/reference/rds-api/datacontrol-object-rds.md)데이터 [집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체에 비동기적으로 데이터를 검색 하는 DataControl 개체입니다. **OnReadyStateChange** 이벤트를 사용 하 여 발생할 때마다 **ReadyState** 속성의 변경 내용을 모니터링 합니다. 이는 주기적으로 속성의 값을 확인 하는 것 보다 효율적입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>참고 항목  
 [ADO Events 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)


