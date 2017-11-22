---
title: 'Ibcpsession:: Bcpexec (OLE DB) | Microsoft Docs'
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-interfaces
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: IBCPSession::BCPExec (OLE DB)
apitype: COM
helpviewer_keywords: BCPExec method
ms.assetid: 0f4ebb63-cf03-4e53-846e-6c3021cde007
caps.latest.revision: "23"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c12b94216591fdf4378db0c03951b7300f2d134d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="ibcpsessionbcpexec-ole-db"></a>IBCPSession::BCPExec(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  대량 복사 작업을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT BCPExec(   
      DBROWCOUNT *pRowsCopied);  
```  
  
## <a name="remarks"></a>주의  
 **BCPExec** 값에 따라 데이터베이스 테이블 또는 그 반대로 사용자 파일에서 데이터를 복사 하는 메서드는 *eDirection* 함께 사용 하는 매개 변수는 [ibcpsession:: Bcpinit](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)메서드.  
  
 호출 하기 전에 **BCPExec**, 호출 된 **BCPInit** 올바른 사용자 파일 이름 사용 하 여 메서드. 그렇게 하지 않으면 오류가 반환됩니다. 단, 쿼리를 대량 복사하기(bulk copy out) 작업에 사용할 경우는 예외입니다. 이 경우 테이블 이름에 대해 NULL을 지정 된 **BCPInit** 메서드 다음 BCP_OPTION_HINTS 옵션을 사용 하 여 쿼리를 지정 합니다.  
  
 **BCPExec** 메서드는 유일한 대량 복사 메서드입니다 오랫동안 보류 될 수 있습니다. 따라서 비동기 모드를 지원하는 유일한 대량 복사 메서드입니다. 비동기 모드를 사용 하려면 공급자 공급자별 세션 속성 SSPROP_ASYNCH_BULKCOPY를 variant_true로 호출 하기 전에 설정의 **BCPExec** 메서드. 이 속성은 DBPROPSET_SQLSERVERSESSION 속성 집합에서 사용할 수 있습니다. 완료를 테스트 하려면 호출는 **BCPExec** 메서드 동일한 매개 변수를 사용 합니다. 대량 복사 아직 완료 되지 않은 경우는 **BCPExec** 메서드는 DB_S_ASYNCHRONOUS를 반환 합니다. 반환은 *pRowsCopied* 인수로 전송 되거나 서버에서 수신 된 행 수의 상태 수입니다. 서버로 전송된 행은 일괄 처리의 끝에 도달할 때까지 커밋되지 않습니다.  
  
## <a name="arguments"></a>인수  
 *pRowsCopied*[out]  
 DWORD에 대한 포인터입니다. **BCPExec** 메서드 성공적으로 복사 된 행 수로 DWORD를 채웁니다. 경우는 *pRowsCopied* 인수는 NULL로 설정 되어에서 무시 되는 **BCPExec** 메서드.  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 메서드가 성공했습니다.  
  
 E_FAIL  
 공급자 관련 오류가 발생 했습니다. 자세한 내용은 사용 하 여는 [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 인터페이스입니다.  
  
 E_UNEXPECTED  
 예기치 않은 메서드가 호출되었습니다. 예를 들어 이 메서드를 호출하기 전에 **BCPInit** 메서드를 호출하지 않았습니다. BCP_OPTION_ABORT 옵션을 사용 하 여 작업이 중단 된 경우에 발생 및 **BCPExec** 메서드가 나중에 호출 되었습니다.  
  
 E_OUTOFMEMORY  
 메모리 부족 오류가 발생했습니다.  
  
 DB_S_ENDOFROWSET  
 대량 복사 작업이 완료되었고 데이터 전송이 모두 완료되었습니다.  
  
 DB_S_ASYNCHRONOUS  
 행의 현재 일괄 처리가 복사되었습니다. 호출 된 **BCPExec** 다시 다음 일괄 처리를 전송할 메서드.  
  
 DB_S_ERRORSOCCURRED  
 대량 복사 작업 동안 오류가 발생하여 일부 행이 복사되지 않았습니다. 오류 수는 아직 허용되는 최대 오류 수보다 적습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [IBCPSession &#40; OLE db&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md)   
 [대량 복사 작업 수행](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
  
  
