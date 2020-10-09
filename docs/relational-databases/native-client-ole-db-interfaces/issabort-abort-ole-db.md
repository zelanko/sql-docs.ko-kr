---
description: 'ISSAbort:: Abort (Native Client OLE DB 공급자)'
title: 'ISSAbort:: Abort (Native Client OLE DB 공급자) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSAbort::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
ms.assetid: a5bca169-694b-4895-84ac-e8fba491e479
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 708d5e0e825e46a6eb2a6c04df08932b780ba3c1
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91866711"
---
# <a name="issabortabort-native-client-ole-db-provider"></a>ISSAbort:: Abort (Native Client OLE DB 공급자)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  현재 행 집합 및 현재 명령과 연결된 일괄 처리되는 명령을 취소합니다.  
  
Native Client OLE DB 공급자에 노출 되는 **ISSAbort** 인터페이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 현재 행 집합을 취소 하는 데 사용 되는 **ISSAbort:: Abort** 메서드와, 처음에 행 집합을 생성 한 명령을 사용 하 여 일괄 처리 되 고 아직 실행이 완료 되지 않은 모든 명령을 제공 합니다.  
  
 **ISSAbort** 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ICommand:: Execute** 또는 **iopenrowset:: OpenRowset**에서 반환 된 **IMultipleResults** 개체에 대해 **QueryInterface** 를 사용 하 여 사용할 수 있는 Native Client 공급자별 인터페이스입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>설명  
 중단 되는 명령이 저장 프로시저에 있는 경우 저장 프로시저 (및 해당 프로시저를 호출한 프로시저)의 실행이 종료 되 고 저장 프로시저 호출을 포함 하는 명령 일괄 처리가 종료 됩니다. 서버에서 결과 집합을 클라이언트로 전송 중이면 전송이 중지됩니다. 클라이언트가 결과 집합을 사용하지 않으려는 경우 행 집합을 해제하기 전에 **ISSAbort::Abort**를 호출하면 행 집합을 신속하게 해제할 수 있습니다. 그러나 열려 있는 트랜잭션이 있고 XACT_ABORT가 ON인 경우 **ISSAbort::Abort**를 호출하면 트랜잭션이 롤백됩니다.  
  
 **ISSAbort::Abort**가 S_OK를 반환한 후에는 연결된 **IMultipleResults** 인터페이스가 사용할 수 없는 상태로 전환되어 해제될 때까지 모든 메서드 호출(**IUnknown** 인터페이스로 정의된 메서드는 제외)에 대해 DB_E_CANCELED를 반환합니다. **Abort**를 호출하기 전에 **IMultipleResults**에서 **IRowset**을 가져온 경우에도 **ISSAbort::Abort** 호출 후 인터페이스가 사용할 수 없는 상태로 전환되어 해제될 때까지 모든 메서드 호출(**IUnknown** 인터페이스 및 **IRowset::ReleaseRows**로 정의된 메서드는 제외)에 대해 DB_E_CANCELED를 반환합니다.  
  
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
 공급자 관련 오류가 발생했습니다. 자세한 내용을 보려면 [ISQLServerErrorInfo](../../connect/oledb/ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md?view=sql-server-ver15) 인터페이스를 사용하세요.  
  
 E_UNEXPECTED  
 예기치 않은 메서드가 호출되었습니다. **ISSAbort::Abort**가 이미 호출되어 개체가 좀비 상태에 있는 경우를 예로 들 수 있습니다.  
  
 E_OUTOFMEMORY  
 메모리 부족 오류가 발생했습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ISSAbort &#40;OLE DB&#41;]()  
  
