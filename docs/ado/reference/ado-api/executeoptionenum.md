---
title: ExecuteOptionEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ExecuteOptionEnum
helpviewer_keywords:
- ExecuteOptionEnum enumeration [ADO]
ms.assetid: 68bfa83a-5df4-4bef-8736-0f88ae8c29ea
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 74248756628e892ff8a00e0e6e206b5eb7639e05
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="executeoptionenum"></a>ExecuteOptionEnum
공급자가 명령을 실행할 방법을 지정 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adAsyncExecute**|0x10|명령을 비동기적으로 실행 해야 나타냅니다.<br /><br /> 이 값을 함께 사용할 수는 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 값 **adCmdTableDirect**합니다.|  
|**adAsyncFetch**|0x20|나머지 행에 지정 된 초기 수량 후 나타냅니다는 [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) 속성을 비동기적으로 검색 해야 합니다.|  
|**adAsyncFetchNonBlocking**|0x40|검색 하는 동안 주 스레드가 차단 되지 않으면 있는지를 나타냅니다. 요청한 행을 검색 하지 자동으로 현재 행 파일의 끝으로 이동 합니다.<br /><br /> 여는 경우는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 에서 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 포함 영구적으로 저장 된 **레코드 집합**, **adAsyncFetchNonBlocking** 수는 없습니다 효과; 작업은 동기식으로 차단 됩니다.<br /><br /> **adAsynchFetchNonBlocking** 이 없는 하면 적용는 [adCmdTableDirect](../../../ado/reference/ado-api/commandtypeenum.md) 옵션 여는 데 사용 되는 **레코드 집합**합니다.|  
|**adExecuteNoRecords**|0x80|명령 텍스트가 명령 또는 행 (예를 들어만 데이터를 삽입 하는 명령)을 반환 하지 않는 저장된 프로시저 임을 나타냅니다. 행이 검색 되는 경우 삭제 되며 반환 되지 않습니다.<br /><br /> **adExecuteNoRecords** 에 선택적 매개 변수로 전달할 수 있습니다는 **명령** 또는 **연결 실행** 메서드.|  
|**adExecuteStream**|0x400|명령 실행의 결과 스트림으로 반환 되어야 함을 나타냅니다.<br /><br /> **adExecuteStream** 에 선택적 매개 변수로 전달할 수 있습니다는 **명령을 실행할** 메서드.|  
|**adExecuteRecord**||나타냅니다는 **CommandText** 명령 또는 단일 행으로 반환 되어야을 반환 하는 저장된 프로시저는 **레코드** 개체입니다.|  
|**adOptionUnspecified**|-1|이 명령은 지정 된 임을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 패키지에 대 한 **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.ExecuteOption.ASYNCEXECUTE|  
|AdoEnums.ExecuteOption.ASYNCFETCH|  
|AdoEnums.ExecuteOption.ASYNCFETCHNONBLOCKING|  
|AdoEnums.ExecuteOption.NORECORDS|  
|AdoEnums.ExecuteOption.UNSPECIFIED|  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Execute 메서드(ADO 명령)](../../../ado/reference/ado-api/execute-method-ado-command.md)|[Execute 메서드(ADO 연결)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|  
|[Open 메서드(ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[Requery 메서드](../../../ado/reference/ado-api/requery-method.md)|

