---
title: 'Issabort:: Abort (OLE DB) | Microsoft Docs'
description: ISSAbort::Abort(OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSAbort::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: fca6371ee81bcf14218c5ea3dd3e2281d0493204
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51602198"
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  현재 행 집합 및 현재 명령과 연결된 일괄 처리되는 명령을 취소합니다.  
  
SQL Server용 OLE DB 드라이버에서 공개된 **ISSAbort** 인터페이스가 제공하는 **ISSAbort::Abort** 메서드를 사용하여 현재 행 집합 및 처음 이 행 집합을 생성한 명령과 함께 일괄 처리되었지만 아직 실행이 완료되지 않은 모든 명령을 취소할 수 있습니다.  
  
 **ISSAbort**는 **ICommand::Execute** 또는 **IOpenRowset::OpenRowset**에 의해 반환되는 **IMultipleResults** 개체의 **QueryInterface**를 통해 사용할 수 있는 SQL Server용 OLE DB 드라이버별 인터페이스입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>Remarks  
 중단할 명령이 저장 프로시저에 있으면 저장 프로시저 및 해당 프로시저를 호출한 프로시저의 실행 및 저장 프로시저 호출이 포함된 명령 일괄 처리가 종료됩니다. 서버에서 결과 집합을 클라이언트로 전송 중이면 이 전송이 중지됩니다. 클라이언트가 결과 집합을 사용하지 않으려는 경우 행 집합을 해제하기 전에 **ISSAbort::Abort**를 호출하면 행 집합을 신속하게 해제할 수 있습니다. 그러나 열려 있는 트랜잭션이 있고 XACT_ABORT가 ON인 경우 **ISSAbort::Abort**를 호출하면 트랜잭션이 롤백됩니다.  
  
 **ISSAbort::Abort**가 S_OK를 반환한 후에는 연결된 **IMultipleResults** 인터페이스가 사용할 수 없는 상태로 전환되어 해제될 때까지 모든 메서드 호출(**IUnknown** 인터페이스로 정의된 메서드는 제외)에 대해 DB_E_CANCELED를 반환합니다. **Abort**를 호출하기 전에 **IMultipleResults**에서 **IRowset**을 가져온 경우에도 **ISSAbort::Abort** 호출 후 인터페이스가 사용할 수 없는 상태로 전환되어 해제될 때까지 모든 메서드 호출(**IUnknown** 인터페이스 및 **IRowset::ReleaseRows**로 정의된 메서드는 제외)에 대해 DB_E_CANCELED를 반환합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]부터는 서버 XACT_ABORT 상태가 ON일 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결되어 있을 때 **ISSAbort::Abort**를 실행하면 현재의 암시적 또는 명시적 트랜잭션이 종료되고 롤백됩니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 현재 트랜잭션이 중단되지 않습니다.  
  
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
 공급자 관련 오류가 발생했습니다. 자세한 내용을 보려면 [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 인터페이스를 사용하십시오.  
  
 E_UNEXPECTED  
 예기치 않은 메서드가 호출되었습니다. **ISSAbort::Abort**가 이미 호출되어 개체가 좀비 상태에 있는 경우를 예로 들 수 있습니다.  
  
 E_OUTOFMEMORY  
 메모리 부족 오류가 발생했습니다.  
  
  
