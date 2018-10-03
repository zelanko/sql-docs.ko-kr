---
title: ISSAsynchStatus (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSAsynchStatus (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- ISSAsynchStatus interface
ms.assetid: c643f09f-9ccc-4d8b-9243-3cde86c2bd46
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aeb6c6c789bfe1ca2af5616fb0a1ef9785700224
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48115023"
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus(OLE DB)
  **ISSAsynchStatus** 에 대 한 지원을 노출 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 비동기 작업입니다. 이 인터페이스는 선택적 인터페이스이며 핵심 OLE DB 인터페이스인 **IDBAsynchStatus**에서 상속됩니다. **ISSAsynchStatus** 는 **IDBAsynchStatus** 에서 상속된 **Abort**및 **GetStatus** 메서드 이외에도 비동기 작업이 완료되거나 제한 시간이 초과될 때까지 대기하는 데 사용되는 새 메서드를 제공합니다.  
  
|메서드|Description|  
|------------|-----------------|  
|[Issasynchstatus:: Abort &#40;OLE DB&#41;](issasynchstatus-abort-ole-db.md)|비동기적으로 실행 중인 작업을 취소합니다.|  
|[Issasynchstatus:: Getstatus &#40;OLE DB&#41;](issasynchstatus-getstatus-ole-db.md)|비동기적으로 실행 중인 작업의 상태를 반환합니다.|  
|[Issasynchstatus:: Waitforasynchcompletion &#40;OLE DB&#41;](issasynchstatus-waitforasynchcompletion-ole-db.md)|비동기적으로 실행 중인 작업이 완료되거나 제한 시간이 초과될 때까지 대기합니다.|  
  
## <a name="remarks"></a>Remarks  
 **ISSAsynchStatus::GetStatus** 메서드의 **ISSAsynchStatus** 구현은 **IDBAsynchStatus::GetStatus** 메서드와 같지만 데이터 원본 개체의 초기화가 중단된 경우 DB_E_CANCELED 대신 E_UNEXPECTED를 반환한다는 점만 다릅니다(단, **ISSAsynchStatus::WaitForAsynchCompletion** 은 DB_E_CANCELED를 반환함). 이는 중단 작업 이후 데이터 원본 개체가 평소의 상태로 유지되지 않아 추가적인 초기화 작업이 시도될 수 있기 때문입니다.  
  
 다음 메서드를 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 비동기적인 실행을 사용할 수 있습니다.  
  
-   **ICommand::Execute**  
  
-   **IOpenRowset::OpenRowset**  
  
-   **IMultipleResults::GetResult**  
  
## <a name="see-also"></a>관련 항목  
 [인터페이스 &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [비동기 작업 수행](../native-client/features/performing-asynchronous-operations.md)  
  
  
