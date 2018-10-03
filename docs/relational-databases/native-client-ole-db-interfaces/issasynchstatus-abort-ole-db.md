---
title: 'Issasynchstatus:: Abort (OLE DB) | Microsoft 문서'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSAsynchStatus::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
ms.assetid: 2a4bd312-839a-45a8-a299-fc8609be9a2a
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9f12cc39f6d3c3b507734d1c7750491aba15ea20
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47640411"
---
# <a name="issasynchstatusabort-ole-db"></a>ISSAsynchStatus::Abort(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

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
 중단할 작업입니다. 값은 다음과 같아야 합니다.  
  
 DBASYNCHOP_OPEN - 취소 요청이 행 집합의 비동기 열기 또는 채우기나 데이터 원본 개체의 비동기 초기화에 적용됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 비동기 작업 취소 요청이 처리되었습니다. 작업 자체가 취소된 것은 아닙니다. 작업이 취소되었는지 확인하려면 소비자가 [ISSAsynchStatus::GetStatus](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-getstatus-ole-db.md) 를 호출하고 DB_E_CANCELED를 확인해야 합니다. 하지만 바로 다음 호출에서 이 값이 반환되지 않을 수도 있습니다.  
  
 DB_E_CANTCANCEL  
 비동기 작업을 취소할 수 없습니다.  
  
 DB_E_CANCELED  
 알림 중에 비동기 작업 중단 요청이 취소되었습니다. 작업이 여전히 비동기적으로 실행되고 있습니다.  
  
 E_FAIL  
 공급자 관련 오류가 발생했습니다.  
  
 E_INVALIDARG  
 *hChapter* 매개 변수가 DB_NULL_HCHAPTER가 아니거나 *eOperation* 이 DBASYNCH_OPEN이 아닙니다.  
  
 E_UNEXPECTED  
 **IDBInitialize::Initialize** 가 취소되지 않은 데이터 원본 개체에서 **ISSAsynchStatus::Abort** 가 호출되었거나 호출이 완료되지 않았습니다.  
  
 **IDBInitialize::Initialize** 가 호출되었지만 초기화 전에 취소된 데이터 원본 개체에서 **ISSAsynchStatus::Abort** 가 호출되었거나 시간이 초과되었습니다. 데이터 원본 개체가 여전히 초기화가 취소되지 않았습니다.  
  
 이전에**ITransaction::Ab가 호출된 행 집합에서t** 또는 **ITransaction::Ab가 호출된 행 집합에서t** 가 호출된 행 집합에서 **ITransaction::Ab가 호출된 행 집합에서t** was previously called, and the rowset did not survive the commit 가 호출된 행 집합에서 ab가 호출된 행 집합에서t and is in a zombie state.  
  
 초기화 단계에서 비동기적으로 취소된 행 집합에서**ISSAsynchStatus::Abort** 가 취소되었습니다. 행 집합이 좀비 상태에 있습니다.  
  
## <a name="remarks"></a>Remarks  
 행 집합이나 데이터 원본 개체의 초기화를 중단하면 행 집합이나 데이터 원본 개체가 좀비 상태로 유지되어 **IUnknown** 메서드가 아닌 모든 메서드에서 E_UNEXPECTED를 반환할 수 있습니다. 이 경우 소비자가 사용할 수 있는 유일한 동작은 행 집합이나 데이터 원본 개체를 해제하는 것입니다.  
  
 **ISSAsynchStatus::Abort** 를 호출하고 DBASYNCHOP_OPEN이 아닌 *eOperation* 값을 전달하면 S_OK가 반환됩니다. 작업이 완료 또는 취소된 것은 아닙니다.  
  
## <a name="see-also"></a>관련 항목  
 [비동기 작업 수행](../../relational-databases/native-client/features/performing-asynchronous-operations.md)  
  
  
