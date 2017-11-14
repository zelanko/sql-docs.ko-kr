---
title: "Cancel 메서드 (RDS) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Cancel method [RDS]
ms.assetid: 560b5b3d-fba9-4275-8920-9c3e186134f7
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 870eeb951d945dd1d24ce35d89156be1971feb26
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="cancel-method-rds"></a>Cancel 메서드 (RDS)
실행을 취소는 보류 중인 비동기 메서드 호출 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RDS.DataControl.Cancel  
```  
  
## <a name="remarks"></a>주의  
 호출 하는 경우 **취소**, [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) 로 자동 설정 됩니다 **adcReadyStateLoaded**, 및 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 비어 있게 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Cancel 메서드 (VBScript) 예제](../../../ado/reference/rds-api/cancel-method-example-vbscript.md)   
 [Cancel 메서드 (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [CancelBatch 메서드 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate 메서드 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [CancelUpdate 메서드 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [ExecuteOptions 속성(RDS)](../../../ado/reference/rds-api/executeoptions-property-rds.md)



