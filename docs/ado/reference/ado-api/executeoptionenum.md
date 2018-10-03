---
title: ExecuteOptionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ExecuteOptionEnum
helpviewer_keywords:
- ExecuteOptionEnum enumeration [ADO]
ms.assetid: 68bfa83a-5df4-4bef-8736-0f88ae8c29ea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7512f456d1423caf6318903119c2ad55c1938dec
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47719121"
---
# <a name="executeoptionenum"></a>ExecuteOptionEnum
공급자 명령 실행 방식을 지정 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adAsyncExecute**|0x10|명령을 비동기적으로 실행 해야 나타냅니다.<br /><br /> 이 값과 결합할 수 없습니다는 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 값 **adCmdTableDirect**합니다.|  
|**adAsyncFetch**|0x20|나머지 행에 지정 된 초기 수량 후 나타냅니다 합니다 [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) 속성 비동기적으로 검색 해야 합니다.|  
|**adAsyncFetchNonBlocking**|0x40|검색 하는 동안 주 스레드가 차단 되지 있는지를 나타냅니다. 요청한 행 검색 되지 않았습니다, 현재 행 파일의 끝에 자동으로 이동 합니다.<br /><br /> 여는 경우는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 에서 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 영구적으로 저장을 포함 하 **레코드 집합**, **adAsyncFetchNonBlocking** 수는 없습니다 효과; 작업이 동기 및 차단 됩니다.<br /><br /> **adAsynchFetchNonBlocking** 가 없는 경우 적용를 [adCmdTableDirect](../../../ado/reference/ado-api/commandtypeenum.md) 옵션은 여는 데 사용 되는 **레코드 집합**합니다.|  
|**adExecuteNoRecords**|0x80|명령 텍스트가 명령 또는 행 (예를 들어만 데이터를 삽입 하는 명령)을 반환 하지 않는 저장된 프로시저 임을 나타냅니다. 모든 행이 검색 하는 경우 삭제 되며 반환 되지 않습니다.<br /><br /> **adExecuteNoRecords** 선택적 매개 변수로 전달할 수 있습니다 합니다 **명령** 또는 **연결 실행** 메서드.|  
|**adExecuteStream**|0x400|명령 실행의 결과 스트림으로 반환 되어야 함을 나타냅니다.<br /><br /> **adExecuteStream** 선택적 매개 변수로 전달할 수 있습니다 합니다 **Command Execute** 메서드.|  
|**adExecuteRecord**||나타내는 합니다 **CommandText** 명령 또는으로 반환 되어야 하는 단일 행을 반환 하는 저장된 프로시저를 **레코드** 개체입니다.|  
|**adOptionUnspecified**|-1|명령이 지정 되지 않음을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 Package: **com.ms.wfc.data**  
  
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
