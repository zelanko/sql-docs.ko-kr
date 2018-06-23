---
title: 'Issabort:: Abort (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ISSAbort::Abort (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- Abort method
ms.assetid: a5bca169-694b-4895-84ac-e8fba491e479
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0729183a2e5be91d3cdb30eae3ae5990f8398103
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172164"
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort(OLE DB)
  현재 행 집합 및 현재 명령과 연결된 일괄 처리되는 명령을 취소합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>Remarks  
 중단할 명령이 저장 프로시저에 있으면 저장 프로시저 및 해당 프로시저를 호출한 프로시저의 실행 및 저장 프로시저 호출이 포함된 명령 일괄 처리가 종료됩니다. 서버에서 결과 집합을 클라이언트로 전송 중이면 전송이 중지됩니다. 클라이언트는 결과 집합을 사용 하지 않으려고, 하는 경우 호출 **issabort:: Abort** 행 집합 릴리스를 신속 하 게 행 집합을 해제 하지만 트랜잭션이 롤백됩니다 열려 있는 트랜잭션이 있고 XACT_ABORT가 ON 될 때 **Issabort:: Abort** 라고  
  
 후 **issabort:: Abort** S_OK를 관련된 된 반환 **IMultipleResults** 사용할 수 없는 상태로 입력 하 고 모든 메서드 호출에 DB_E_CANCELED를 반환 하는 인터페이스 ( 는여정의된메서드를제외하고**IUnknown** 인터페이스) 해제 될 때까지 합니다. 경우는 **IRowset** 에서 가져온 **IMultipleResults** 를 호출 하기 전에 **중단**도 사용할 수 없는 상태로 전환 하 고 (호출 하는 모든 메서드에 DB_E_CANCELED를 반환 정의한 메서드를 제외 하 고는 **IUnknown** 인터페이스 및 **irowset:: Releaserows**)을 성공적으로 호출한 후에 해제 될 때까지 **issabort:: Abort** .  
  
> [!NOTE]  
>  부터는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]서버 XACT_ABORT 상태가에 있으면, 실행, **issabort:: Abort** 종료 되 고에 연결 된 경우 모든 현재 암시적 또는 명시적 트랜잭션을 롤백하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 현재 트랜잭션이 중단되지 않습니다.  
  
## <a name="arguments"></a>인수  
 없음  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 **issabort:: Abort** 메서드 일괄 처리가 취소 된 경우 S_OK와 DB_E_CANTCANCEL 그렇지 않으면 반환 합니다. 일괄 처리가 이미 취소되었으면 DB_E_CANCELED가 반환됩니다.  
  
 DB_E_CANCELED  
 일괄 처리가 이미 취소되었습니다.  
  
 DB_E_CANTCANCEL  
 일괄 처리가 취소되지 않았습니다.  
  
 E_FAIL  
 공급자 관련 오류가 발생 했습니다. 자세한 내용은 사용 하 여는 [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) 인터페이스입니다.  
  
 E_UNEXPECTED  
 예기치 않은 메서드가 호출되었습니다. 예를 들어 개체가 좀비 상태에서 이므로 **issabort:: Abort** 가 이미 호출 되었습니다.  
  
 E_OUTOFMEMORY  
 메모리 부족 오류가 발생했습니다.  
  
## <a name="see-also"></a>관련 항목  
 [ISSAbort &#40;OLE DB&#41;](../../database-engine/dev-guide/issabort-ole-db.md)  
  
  