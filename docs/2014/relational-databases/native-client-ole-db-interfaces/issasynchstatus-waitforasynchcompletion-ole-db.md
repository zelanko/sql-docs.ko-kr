---
title: 'ISSAsynchStatus:: WaitForAsynchCompletion (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- WaitForAsynchCompletion method
ms.assetid: 9f65e9e7-eb93-47a1-bc42-acd4649fbd0e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: af77f5f5519a49e2d9a744dceca2857cc88ce8e1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63192315"
---
# <a name="issasynchstatuswaitforasynchcompletion-ole-db"></a>ISSAsynchStatus::WaitForAsynchCompletion(OLE DB)
  비동기적으로 실행 중인 작업이 완료되거나 제한 시간이 초과될 때까지 대기합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT WaitForAsynchCompletion(   
  DWORD dwMillisecTimeOut);  
```  
  
## <a name="arguments"></a>인수  
 *dwMillisecTimeOut*[in]  
 제한 시간(밀리초)입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 메서드가 성공했습니다.  
  
 E_UNEXPECTED  
 
  **ITransaction::Commit** 또는 **ITransaction::Abort** 가 호출되었거나 행 집합이 초기화 단계 중 취소되었기 때문에 행 집합이 사용되지 않은 상태입니다.  
  
 DB_E_CANCELED  
 행 집합 채우기 또는 데이터 원본 개체 초기화 중 비동기 처리가 취소되었습니다.  
  
 DB_S_ASYNCHRONOUS  
 지정한 제한 시간에 도달했지만 작업이 완료되지 않았습니다.  
  
> [!NOTE]  
>  위에 나열된 반환 코드 값 외에도 **ISSAsynchStatus::WaitForAsynchCompletion** 메서드는 코어 OLEDB **ICommand::Execute** 및 **IDBInitialize::Initialize** 메서드에서 반환하는 반환 코드 값을 지원합니다.  
  
## <a name="remarks"></a>설명  
 
  **ISSAsynchStatus::WaitForAsynchCompletion** 메서드는 제한 시간 값(밀리초)이 경과하거나 보류 중인 작업이 완료될 때까지 값을 반환하지 않습니다. **Command** 개체에는 시간이 초과 되기 전에 쿼리가 실행 되는 시간 (초)을 제어 하는 **CommandTimeout** 속성이 있습니다. **ISSAsynchStatus:: WaitForAsynchCompletion** 메서드와 함께 사용 하는 경우 **CommandTimeout** 속성은 무시 됩니다.  
  
 비동기 작업의 경우 제한 시간 속성이 무시됩니다. 
  **ISSAsynchStatus::WaitForAsynchCompletion** 의 제한 시간 매개 변수는 컨트롤이 호출자에게 반환되기 전까지의 최대 경과 시간을 지정합니다. 제한 시간이 만료되면 DB_S_ASYNCHRONOUS가 반환됩니다. 제한 시간을 지정해도 비동기 작업이 취소되지 않습니다. 애플리케이션이 제한 시간 내에 완료되지 않은 비동기 작업을 취소해야 할 경우 애플리케이션은 제한 시간에 도달할 때까지 기다린 다음 DB_S_ASYNCHRONOUS가 반환되면 작업을 명시적으로 취소해야 합니다.  
  
> [!NOTE]  
>  OLE DB Service Component를 사용하는 경우 DB_S_ASYNCHRONOUS 대신 S_OK가 반환될 수 있으므로 S_OK 또는 DB_S_ASYNCHRONOUS가 반환되는 경우 애플리케이션은 [ISSAsynchStatus::GetStatus](issasynchstatus-getstatus-ole-db.md) 를 호출하여 완료 여부를 확인해야 합니다.  
  
 
  *dwMillisecTimeOut* 값이 INFINITE로 설정되면 작업이 완료될 때까지 **ISSAsynchStatus::WaitForAsynchCompletion** 메서드가 차단됩니다. 
  *dwMillisecTimeOut* 값이 0으로 설정되면 보류 중인 작업의 상태와 함께 메서드가 즉시 반환됩니다. 작업이 완료되기 전에 제한 시간이 만료되면 DB_S_ASYNCHRONOUS가 반환됩니다.  
  
 제한 시간이 만료되기 전에 작업이 완료되면 반환되는 HRESULT는 작업이 반환하는 HRESULT(작업이 동기적으로 수행된 경우 반환되는 HRESULT)입니다.  
  
 또한 SSPROP_ISSAsynchStatus 속성이 DBPROPSET_SQLSERVERROWSET 속성 집합에 추가되었습니다. 
  [ISSAsynchStatus](issasynchstatus-ole-db.md) 인터페이스를 지원하는 공급자는 VARIANT_TRUE 값을 사용하여 이 속성을 구현해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [비동기 작업 수행](../native-client/features/performing-asynchronous-operations.md)   
 [ISSAsynchStatus &#40;OLE DB&#41;](issasynchstatus-ole-db.md)  
  
  
