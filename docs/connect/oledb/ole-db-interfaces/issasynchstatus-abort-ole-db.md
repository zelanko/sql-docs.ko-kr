---
title: 'ISSAsynchStatus:: Abort (OLE DB) | Microsoft Docs'
description: ISSAsynchStatus::Abort(OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSAsynchStatus::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 4cb57bfac5af957bd9f2f539b025f32b5f481d66
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015431"
---
# <a name="issasynchstatusabort-ole-db"></a>ISSAsynchStatus::Abort(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  비동기적으로 실행 중인 작업을 취소합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT Abort(  
        HCHAPTER hChapter,  
        DBASYNCHOP eOperation);  
```  
  
## <a name="arguments"></a>인수  
 *hChapter*[in]  
 작업을 중단할 장의 처리기입니다. 호출되는 개체가 행 집합 개체가 아니거나 작업이 장에 적용되지 않는 경우 호출자가 *hChapter* 를 DB_NULL_HCHAPTER로 설정해야 합니다.  
  
 *eOperation*[in]  
 중단할 작업입니다. 다음 값을 사용 해야 합니다.  
  
 DBASYNCHOP_OPEN - 취소 요청이 행 세트의 비동기 열기 또는 채우기나 데이터 원본 개체의 비동기 초기화에 적용됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 비동기 작업 취소 요청이 처리되었습니다. 작업 자체가 취소된 것은 아닙니다. 작업이 취소되었는지 확인하려면 소비자가 [ISSAsynchStatus::GetStatus](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md) 를 호출하고 DB_E_CANCELED를 확인해야 합니다. 하지만 바로 다음 호출에서 이 값이 반환되지 않을 수도 있습니다.  
  
 DB_E_CANTCANCEL  
 비동기 작업을 취소할 수 없습니다.  
  
 DB_E_CANCELED  
 알림 중에 비동기 작업 중단 요청이 취소되었습니다. 작업이 여전히 비동기적으로 실행되고 있습니다.  
  
 E_FAIL  
 공급자 관련 오류가 발생했습니다.  
  
 E_INVALIDARG  
 *hChapter* 매개 변수가 DB_NULL_HCHAPTER가 아니거나 *eOperation*이 DBASYNCH_OPEN이 아닙니다.  
  
 E_UNEXPECTED  
 **IDBInitialize::Initialize**가 호출되지 않았거나 호출이 완료되지 않은 데이터 원본 개체에서 **ISSAsynchStatus::Abort**가 호출되었습니다.  
  
 **IDBInitialize::Initialize** 가 호출되었지만 초기화 전에 취소된 데이터 원본 개체에서 **ISSAsynchStatus::Abort** 가 호출되었거나 시간이 초과되었습니다. 데이터 원본 개체가 여전히 초기화가 취소되지 않았습니다.  
  
 이전에 **ITransaction::Commit** 또는 **ITransaction::Abort**가 호출된 행 집합에서 **ISSAsynchStatus::Abort**가 호출되었으며, 행 집합이 커밋 또는 중단 후에 유지되지 않아 좀비 상태에 있습니다.  
  
 초기화 단계에서 비동기적으로 취소된 행 집합에서**ISSAsynchStatus::Abort** 가 취소되었습니다. 행 집합이 좀비 상태에 있습니다.  
  
## <a name="remarks"></a>Remarks  
 행 집합이나 데이터 원본 개체의 초기화를 중단하면 행 집합이나 데이터 원본 개체가 좀비 상태로 유지되어 **IUnknown** 메서드가 아닌 모든 메서드에서 E_UNEXPECTED를 반환할 수 있습니다. 이 경우 소비자가 사용할 수 있는 유일한 동작은 행 집합이나 데이터 원본 개체를 해제하는 것입니다.  
  
 **ISSAsynchStatus::Abort** 를 호출하고 DBASYNCHOP_OPEN이 아닌 *eOperation* 값을 전달하면 S_OK가 반환됩니다. 작업이 완료 또는 취소된 것은 아닙니다.  
  
## <a name="see-also"></a>참고 항목  
 [비동기 작업 수행](../../oledb/features/performing-asynchronous-operations.md)  
  
  
