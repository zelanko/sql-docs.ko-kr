---
title: 'Issabort:: Abort (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAbort::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
ms.assetid: a5bca169-694b-4895-84ac-e8fba491e479
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 90fdb17506d624e5210288716736ae29721c0feb
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37431262"
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  현재 행 집합 및 현재 명령과 연결된 일괄 처리되는 명령을 취소합니다.  
  
**ISSAbort** 인터페이스에 노출 되는 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 제공 합니다 **issabort:: Abort** 메서드는 현재 행 집합 및 모든 명령을 취소 하는 데 사용 되는 일괄 처리 명령을 사용 하 여 처음에 행 집합을 생성 및 실행을 아직 완료 되지 않은 합니다.  
  
 **ISSAbort** 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 공급자별 인터페이스를 사용 하 여 사용 가능한 **QueryInterface** 에 **IMultipleResults** 반환한 개체  **Icommand:: Execute** 나 **iopenrowset:: Openrowset**합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>Remarks  
 중단할 명령이 저장 프로시저에 있으면 저장 프로시저 및 해당 프로시저를 호출한 프로시저의 실행 및 저장 프로시저 호출이 포함된 명령 일괄 처리가 종료됩니다. 서버에서 결과 집합을 클라이언트로 전송 중이면 전송이 중지됩니다. 클라이언트는 결과 집합을 사용 하려면, 호출 **issabort:: Abort** 행 집합 릴리스 속도 행 집합을 해제 하지만 트랜잭션을 롤백할 수는 열려 있는 트랜잭션이 있고 XACT_ABORT가 ON, 전에 될 때 **Issabort:: Abort** 라고  
  
 이후에 **issabort:: Abort** S_OK를 연결된 된 반환 **IMultipleResults** 인터페이스를 사용할 수 없는 상태를 입력 하 고 모든 메서드 호출에 DB_E_CANCELED를 반환 합니다 (합니다 정의한메서드를제외하고**IUnknown** 인터페이스) 해제 될 때까지 합니다. 경우는 **IRowset** 에서 가져온 **IMultipleResults** 를 호출 하기 전에 **중단**, 또한를 사용할 수 없는 상태에 들어갈 및 모든 메서드로 DB_E_CANCELED를 반환 합니다 (호출 정의한 메서드를 제외 하 고는 **IUnknown** 인터페이스와 **irowset:: Releaserows**) 호출에 성공한 후 해제 될 때까지 **issabort:: Abort** .  
  
> [!NOTE]  
>  부터는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]XACT_ABORT 상태 서버가를 실행 하는 경우 **issabort:: Abort** 종료 되 고 연결할 때 모든 현재 암시적 또는 명시적 트랜잭션을 롤백하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 현재 트랜잭션이 중단되지 않습니다.  
  
## <a name="arguments"></a>인수  
 없음  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 합니다 **issabort:: Abort** 일괄 처리가 취소 된 경우 S_OK와 DB_E_CANTCANCEL 반환 그렇지 않은 경우. 일괄 처리가 이미 취소되었으면 DB_E_CANCELED가 반환됩니다.  
  
 DB_E_CANCELED  
 일괄 처리가 이미 취소되었습니다.  
  
 DB_E_CANTCANCEL  
 일괄 처리가 취소되지 않았습니다.  
  
 E_FAIL  
 공급자 관련 오류가 발생 했습니다. 자세한 내용은 다음을 사용 합니다 [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 인터페이스입니다.  
  
 E_UNEXPECTED  
 예기치 않은 메서드가 호출되었습니다. 예를 들어 개체가 좀비 상태에 있으므로 **issabort:: Abort** 가 이미 호출 되었습니다.  
  
 E_OUTOFMEMORY  
 메모리 부족 오류가 발생했습니다.  
  
## <a name="see-also"></a>관련 항목  
 [ISSAbort &#40;OLE DB&#41;](http://msdn.microsoft.com/library/7c4df482-4a83-4da0-802b-3637b507693a)  
  
  
