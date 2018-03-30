---
title: ISSAsynchStatus (OLE DB) | Microsoft Docs
description: ISSAsynchStatus(OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
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
- ISSAsynchStatus (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSAsynchStatus interface
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 48c141ef28cb51ece708048e568be19d598aff93
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2018
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **ISSAsynchStatus** 인터페이스에 대 한 지원을 노출 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 비동기 작업입니다. 핵심 OLE DB 인터페이스에서 상속 되는 선택적 인터페이스 **IDBAsynchStatus**합니다. **ISSAsynchStatus** 는 **IDBAsynchStatus** 에서 상속된 **Abort**및 **GetStatus** 메서드 이외에도 비동기 작업이 완료되거나 제한 시간이 초과될 때까지 대기하는 데 사용되는 새 메서드를 제공합니다.  
  
|메서드|Description|  
|------------|-----------------|  
|[Issasynchstatus:: Abort &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-abort-ole-db.md)|비동기적으로 실행 중인 작업을 취소합니다.|  
|[Issasynchstatus:: Getstatus &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md)|비동기적으로 실행 중인 작업의 상태를 반환합니다.|  
|[Issasynchstatus:: Waitforasynchcompletion &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)|비동기적으로 실행 중인 작업이 완료되거나 제한 시간이 초과될 때까지 대기합니다.|  
  
## <a name="remarks"></a>주의  
 **ISSAsynchStatus::GetStatus** 메서드의 **ISSAsynchStatus** 구현은 **IDBAsynchStatus::GetStatus** 메서드와 같지만 데이터 원본 개체의 초기화가 중단된 경우 DB_E_CANCELED 대신 E_UNEXPECTED를 반환한다는 점만 다릅니다(단, **ISSAsynchStatus::WaitForAsynchCompletion** 은 DB_E_CANCELED를 반환함). 추가적인 초기화 작업이 시도 될 수 있도록 데이터 원본 개체가 평소의 상태로 중단 작업에서 유지 되지 않습니다 때문입니다.  
  
 다음 메서드를 사용하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 비동기적인 실행을 사용할 수 있습니다.  
  
-   **ICommand::Execute**  
  
-   **IOpenRowset::OpenRowset**  
  
-   **IMultipleResults::GetResult**  
  
## <a name="see-also"></a>관련 항목:  
 [인터페이스 &#40; OLE db&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)    
 [비동기 작업 수행](../../oledb/features/performing-asynchronous-operations.md)  
  
  
