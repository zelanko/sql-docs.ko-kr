---
title: 'Issasynchstatus:: Waitforasynchcompletion (OLE DB) | Microsoft Docs'
description: ISSAsynchStatus::WaitForAsynchCompletion(OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
apitype: COM
helpviewer_keywords:
- WaitForAsynchCompletion method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: d89166474b761f19ae43a9ce0d63f97312a9b3b0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="issasynchstatuswaitforasynchcompletion-ole-db"></a>ISSAsynchStatus::WaitForAsynchCompletion(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
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
 때문에 사용 되지 않은 상태에서 행 집합은 **itransaction:: Commit** 또는 **itransaction:: Abort** 호출한 했거나 행 집합이 초기화 단계 중 취소 되었습니다.  
  
 DB_E_CANCELED  
 행 집합 채우기 또는 데이터 원본 개체가 초기화 중 비동기 처리가 취소 되었습니다.  
  
 DB_S_ASYNCHRONOUS  
 지정한 제한 시간에 도달했지만 작업이 완료되지 않았습니다.  
  
> [!NOTE]  
>  위에 나열된 반환 코드 값 외에도 **ISSAsynchStatus::WaitForAsynchCompletion** 메서드는 코어 OLEDB **ICommand::Execute** 및 **IDBInitialize::Initialize** 메서드에서 반환하는 반환 코드 값을 지원합니다.  
  
## <a name="remarks"></a>주의  
 **ISSAsynchStatus::WaitForAsynchCompletion** 메서드는 제한 시간 값(밀리초)이 경과하거나 보류 중인 작업이 완료될 때까지 값을 반환하지 않습니다. **Command** 개체에는 제한 시간이 초과되기 전까지의 쿼리 실행 시간(초)을 제어하는 **CommandTimeout** 속성이 있습니다. **CommandTimeout** 속성을 **ISSAsynchStatus::WaitForAsynchCompletion** 메서드와 함께 사용하면 이 속성이 무시됩니다.  
  
 비동기 작업의 경우 제한 시간 속성이 무시됩니다. **ISSAsynchStatus::WaitForAsynchCompletion** 의 제한 시간 매개 변수는 컨트롤이 호출자에게 반환되기 전까지의 최대 경과 시간을 지정합니다. 제한 시간이 만료되면 DB_S_ASYNCHRONOUS가 반환됩니다. 제한 시간을 지정해도 비동기 작업이 취소되지 않습니다. 응용 프로그램이 제한 시간 내에 완료되지 않은 비동기 작업을 취소해야 할 경우 응용 프로그램은 제한 시간에 도달할 때까지 기다린 다음 DB_S_ASYNCHRONOUS가 반환되면 작업을 명시적으로 취소해야 합니다.  
  
> [!NOTE]  
>  OLE DB Service Component를 사용하는 경우 DB_S_ASYNCHRONOUS 대신 S_OK가 반환될 수 있으므로 S_OK 또는 DB_S_ASYNCHRONOUS가 반환되는 경우 응용 프로그램은 [ISSAsynchStatus::GetStatus](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md) 를 호출하여 완료 여부를 확인해야 합니다.  
  
 *dwMillisecTimeOut* 값이 INFINITE로 설정되면 작업이 완료될 때까지 **ISSAsynchStatus::WaitForAsynchCompletion** 메서드가 차단됩니다. *dwMillisecTimeOut* 값이 0으로 설정되면 보류 중인 작업의 상태와 함께 메서드가 즉시 반환됩니다. 제한 시간에 작업이 완료 되기 전에 만료 되 면 DB_S_ASYNCHRONOUS가 반환 됩니다.  
  
 제한 시간이 만료되기 전에 작업이 완료되면 반환되는 HRESULT는 작업이 반환하는 HRESULT(작업이 동기적으로 수행된 경우 반환되는 HRESULT)입니다.  
  
 또한 SSPROP_ISSAsynchStatus 속성이 DBPROPSET_SQLSERVERROWSET 속성 집합에 추가되었습니다. [ISSAsynchStatus](../../oledb/ole-db-interfaces/issasynchstatus-ole-db.md) 인터페이스를 지원하는 공급자는 VARIANT_TRUE 값을 사용하여 이 속성을 구현해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [비동기 작업을 수행](../../oledb/features/performing-asynchronous-operations.md)   
 [ISSAsynchStatus & #40; OLE db& #41;](../../oledb/ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  
