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
author: rothja
ms.author: jroth
ms.openlocfilehash: 868acb8dec7ed8a6bd22f3cc5551dede63a50408
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82757139"
---
# <a name="executeoptionenum"></a>ExecuteOptionEnum
공급자가 명령을 실행 하는 방법을 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adAsyncExecute**|0x10|명령을 비동기적으로 실행 해야 함을 나타냅니다.<br /><br /> 이 값은 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 값 **adCmdTableDirect**와 함께 사용할 수 없습니다.|  
|**adAsyncFetch**|0x20|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) 속성에 지정 된 초기 수량 이후의 나머지 행을 비동기식으로 검색 해야 함을 나타냅니다.|  
|**adAsyncFetchNonBlocking**|0x40|는 검색 하는 동안 주 스레드가 차단 되지 않음을 나타냅니다. 요청 된 행을 검색 하지 않은 경우에는 현재 행이 자동으로 파일의 끝으로 이동 합니다.<br /><br /> 영구적으로 저장 된 **레코드 집합**을 포함 하는 [스트림에서](../../../ado/reference/ado-api/stream-object-ado.md) [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 을 여는 경우 **adasyncfetchnonblocking** 은 효과가 없습니다. 작업은 동기식 이며 차단 됩니다.<br /><br /> **adAsynchFetchNonBlocking** 는 [adCmdTableDirect](../../../ado/reference/ado-api/commandtypeenum.md) 옵션을 사용 하 여 **레코드 집합**을 열 때 영향을 주지 않습니다.|  
|**adExecuteNoRecords**|0x80|명령 텍스트가 행을 반환 하지 않는 명령 또는 저장 프로시저 임을 나타냅니다. 예를 들어 데이터만 삽입 하는 명령입니다. 검색 된 행은 삭제 되 고 반환 되지 않습니다.<br /><br /> **adExecuteNoRecords** 는 **명령** 또는 **연결 실행** 메서드에 선택적 매개 변수로 전달 될 수 있습니다.|  
|**adExecuteStream**|0x400|명령 실행 결과를 스트림으로 반환 해야 함을 나타냅니다.<br /><br /> **adExecuteStream** 는 **명령 실행** 메서드에 선택적 매개 변수로 전달 될 수 있습니다.|  
|**adExecuteRecord**||**CommandText** 가 **Record** 개체로 반환 되어야 하는 단일 행을 반환 하는 명령 또는 저장 프로시저 임을 나타냅니다.|  
|**Ado 지정 되지 않음**|-1|명령이 지정 되지 않았음을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums 옵션. ASYNCEXECUTE|  
|AdoEnums 인출|  
|AdoEnums 옵션. ASYNCFETCHNONBLOCKING|  
|AdoEnums. NORECORDS|  
|AdoEnums 옵션입니다. 지정 되지 않았습니다.|  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Execute 메서드(ADO 명령)](../../../ado/reference/ado-api/execute-method-ado-command.md)|[Execute 메서드(ADO 연결)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|  
|[Open 메서드(ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[Requery 메서드](../../../ado/reference/ado-api/requery-method.md)|
