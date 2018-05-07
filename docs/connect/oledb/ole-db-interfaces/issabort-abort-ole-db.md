---
title: 'Issabort:: Abort (OLE DB) | Microsoft Docs'
description: ISSAbort::Abort(OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAbort::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 444d51aeae49e9e626b0666904584bae8e2de6b6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  현재 행 집합 및 현재 명령과 연결된 일괄 처리되는 명령을 취소합니다.  
  
**ISSAbort** 노출 되는 OLE DB 드라이버에서 SQL Server에 대 한 인터페이스를 제공는 **issabort:: Abort** 명령을 사용 하 여 일괄 처리는 현재 행 집합 및 모든 명령을 취소 하는 데 사용 되는 메서드 처음에 행 집합을 생성 하 고 실행을 아직 완료 되지 않은 합니다.  
  
 **ISSAbort** ´ ï ´는 OLE DB Driver for SQL Server 관련 인터페이스를 사용 하 여 **QueryInterface** 에 **IMultipleResults** 에서 반환 된 개체 **icommand:: Execute**  또는 **iopenrowset:: Openrowset**합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>주의  
 중단할 명령이 저장된 프로시저에 있으면 저장된 프로시저 (및 모든 프로시저를 해당 프로시저를 호출한)의 실행 저장된 프로시저 호출을 포함 하는 명령 일괄 처리가 종료 됩니다. 서버가 결과 집합을 클라이언트로 전송 중이면 전송이, 전송이 중지 됩니다. 클라이언트는 결과 집합을 사용 하지 않으려고, 하는 경우 호출 **issabort:: Abort** 행 집합 릴리스를 신속 하 게 행 집합을 해제 하지만 트랜잭션이 롤백됩니다 열려 있는 트랜잭션이 있고 XACT_ABORT가 ON 면 **issabort:: Abort** 라고  
  
 후 **issabort:: Abort** S_OK를 관련된 된 반환 **IMultipleResults** 불안정 한 상태가 입력 하 고 모든 메서드 호출에 DB_E_CANCELED를 반환 하는 인터페이스 ( 는여정의된메서드를제외하고**IUnknown** 인터페이스) 해제 될 때까지 합니다. 경우는 **IRowset** 에서 가져온 **IMultipleResults** 를 호출 하기 전에 **중단**도 사용할 수 없는 상태로 전환 하 고 모든 메서드 호출에 DB_E_CANCELED를 반환 (정의한 메서드를 제외 하 고는 **IUnknown** 인터페이스 및 **irowset:: Releaserows**)을 성공적으로 호출한 후에 해제 될 때까지 **issabort:: Abort**합니다.  
  
> [!NOTE]  
>  부터는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]서버 XACT_ABORT 상태가에 있으면, 실행, **issabort:: Abort** 종료 되 고에 연결 된 경우 모든 현재 암시적 또는 명시적 트랜잭션을 롤백하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 현재 트랜잭션이 중단되지 않습니다.  
  
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
 공급자 관련 오류가 발생 했습니다. 자세한 내용은 사용 하 여는 [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 인터페이스입니다.  
  
 E_UNEXPECTED  
 예기치 않은 메서드가 호출되었습니다. 예를 들어 개체가 좀비 상태에서 이므로 **issabort:: Abort** 가 이미 호출 되었습니다.  
  
 E_OUTOFMEMORY  
 메모리 부족 오류가 발생했습니다.  
  
  
