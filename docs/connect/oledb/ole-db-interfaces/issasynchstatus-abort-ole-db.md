---
title: 'Issasynchstatus:: Abort (OLE DB) | Microsoft Docs'
description: ISSAsynchStatus::Abort(OLE DB)
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
- ISSAsynchStatus::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 09f95f302ba7ee61fa35d7930d4a783ee43194fb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="issasynchstatusabort-ole-db"></a>ISSAsynchStatus::Abort(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  비동기적으로 실행 중인 작업을 취소합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT Abort(  
        HCHAPTER hChapter,  
        DBASYNCHOP eOperation);  
```  
  
## <a name="arguments"></a>인수  
 *hChapter*[in]  
 작업을 중단할 장의 처리기입니다. 호출 되는 개체가 행 집합 개체가 아닙니다 나 작업이 장에 적용 되지 않습니다를 호출자에 게 설정 해야 *hChapter* db_null_hchapter 합니다.  
  
 *eOperation*[in]  
 중단할 작업입니다. 다음 값을 사용 되어야 합니다.  
  
 DBASYNCHOP_OPEN - 취소 요청이 행 집합의 비동기 열기 또는 채우기나 데이터 원본 개체의 비동기 초기화에 적용됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 비동기 작업 취소 요청이 처리되었습니다. 작업 자체가 취소 있는지는 보장 하지 않습니다. 작업이 취소되었는지 확인하려면 소비자가 [ISSAsynchStatus::GetStatus](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md) 를 호출하고 DB_E_CANCELED를 확인해야 합니다. 하지만 바로 다음 호출에서 이 값이 반환되지 않을 수도 있습니다.  
  
 DB_E_CANTCANCEL  
 비동기 작업을 취소할 수 없습니다.  
  
 DB_E_CANCELED  
 알림 중에 비동기 작업 중단 요청이 취소되었습니다. 작업이 여전히 비동기적으로 실행되고 있습니다.  
  
 E_FAIL  
 공급자 관련 오류가 발생했습니다.  
  
 E_INVALIDARG  
 *hChapter* 매개 변수 없는 DB_NULL_HCHAPTER 또는 *eOperation* dbasynch_open이 되지 않습니다.  
  
 E_UNEXPECTED  
 **Issasynchstatus:: Abort** 데이터 원본 개체에서 호출한 **idbinitialize:: Initialize** 호출 되지 않은 또는 완료 되지 않았습니다.  
  
 **IDBInitialize::Initialize** 가 호출되었지만 초기화 전에 취소된 데이터 원본 개체에서 **ISSAsynchStatus::Abort** 가 호출되었거나 시간이 초과되었습니다. 데이터 원본 개체가 여전히 초기화가 취소되지 않았습니다.  
  
 **Issasynchstatus:: Abort** 를 행 집합에서 호출 된 **itransaction:: Commit** 또는 **itransaction:: Abort** 가 이전에 호출 및 행 집합 커밋 또는 중단 하지는 좀비 상태입니다.  
  
 초기화 단계에서 비동기적으로 취소된 행 집합에서**ISSAsynchStatus::Abort** 가 취소되었습니다. 행 집합이 좀비 상태에 있습니다.  
  
## <a name="remarks"></a>주의  
 행 집합이나 데이터 원본 개체의 초기화를 중단하면 행 집합이나 데이터 원본 개체가 좀비 상태로 유지되어 **IUnknown** 메서드가 아닌 모든 메서드에서 E_UNEXPECTED를 반환할 수 있습니다. 이 경우 소비자가 사용할 수 있는 유일한 동작은 행 집합이나 데이터 원본 개체를 해제하는 것입니다.  
  
 **ISSAsynchStatus::Abort** 를 호출하고 DBASYNCHOP_OPEN이 아닌 *eOperation* 값을 전달하면 S_OK가 반환됩니다. 이 작업을 완료 또는 취소 의미 하지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [비동기 작업 수행](../../oledb/features/performing-asynchronous-operations.md)  
  
  
