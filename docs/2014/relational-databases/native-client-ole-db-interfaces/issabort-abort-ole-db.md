---
title: ISSAbort::Abort(OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSAbort::Abort (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- Abort method
ms.assetid: a5bca169-694b-4895-84ac-e8fba491e479
author: rothja
ms.author: jroth
ms.openlocfilehash: a2055514d3ce5e2fdc9d6220a79f489fc64e9c55
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056151"
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort(OLE DB)
  현재 행 집합 및 현재 명령과 연결된 일괄 처리되는 명령을 취소합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>설명  
 중단할 명령이 저장 프로시저에 있으면 저장 프로시저 및 해당 프로시저를 호출한 프로시저의 실행 및 저장 프로시저 호출이 포함된 명령 일괄 처리가 종료됩니다. 서버에서 결과 집합을 클라이언트로 전송 중이면 전송이 중지됩니다. 클라이언트가 결과 집합을 사용하지 않으려는 경우 행 집합을 해제하기 전에 **ISSAbort::Abort**를 호출하면 행 집합을 신속하게 해제할 수 있습니다. 그러나 열려 있는 트랜잭션이 있고 XACT_ABORT가 ON인 경우 **ISSAbort::Abort**를 호출하면 트랜잭션이 롤백됩니다.  
  
 **ISSAbort:: Abort** 가 S_OK를 반환 하면 연결 된 **IMultipleResults** 인터페이스가 사용할 수 없는 상태로 전환 되 고 해제 될 때까지 모든 메서드 호출 ( **IUnknown** 인터페이스에 의해 정의 된 메서드 제외)에 DB_E_CANCELED 반환 됩니다. **Abort**를 호출하기 전에 **IMultipleResults**에서 **IRowset**을 가져온 경우에도 **ISSAbort::Abort** 호출 후 인터페이스가 사용할 수 없는 상태로 전환되어 해제될 때까지 모든 메서드 호출(**IUnknown** 인터페이스 및 **IRowset::ReleaseRows**로 정의된 메서드는 제외)에 대해 DB_E_CANCELED를 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터는 서버 XACT_ABORT 상태가 ON일 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결되어 있을 때 **ISSAbort::Abort**를 실행하면 현재의 암시적 또는 명시적 트랜잭션이 종료되고 롤백됩니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 현재 트랜잭션이 중단되지 않습니다.  
  
## <a name="arguments"></a>인수  
 없음  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 일괄 처리가 취소되었으면 **ISSAbort::Abort** 메서드가 S_OK를 반환하고, 그렇지 않으면 DB_E_CANTCANCEL을 반환합니다. 일괄 처리가 이미 취소되었으면 DB_E_CANCELED가 반환됩니다.  
  
 DB_E_CANCELED  
 일괄 처리가 이미 취소되었습니다.  
  
 DB_E_CANTCANCEL  
 일괄 처리가 취소되지 않았습니다.  
  
 E_FAIL  
 공급자별 오류가 발생 했습니다. 자세한 내용은 [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) 인터페이스를 사용 합니다.  
  
 E_UNEXPECTED  
 예기치 않은 메서드가 호출되었습니다. **ISSAbort::Abort**가 이미 호출되어 개체가 좀비 상태에 있는 경우를 예로 들 수 있습니다.  
  
 E_OUTOFMEMORY  
 메모리 부족 오류가 발생했습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ISSAbort &#40;OLE DB&#41;](../../database-engine/dev-guide/issabort-ole-db.md)  
  
  
