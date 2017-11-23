---
title: bcp_colptr | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: bcp_colptr
apilocation: sqlncli11.dll
apitype: DLLExport
helpviewer_keywords: bcp_colptr function
ms.assetid: 02ece13e-1da3-4f9d-b860-3177e43d2471
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1ddc9f3139136383e5a4f37b827f6d2c12ecf2c5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="bcpcolptr"></a>bcp_colptr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  현재 복사본의 프로그램 변수 데이터 주소를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE bcp_colptr (  
        HDBC hdbc,  
        LPCBYTE pData,  
        INT idxServerCol);  
```  
  
## <a name="arguments"></a>인수  
 *hdbc*  
 대량 복사가 가능한 ODBC 연결 핸들입니다.  
  
 *pData*  
 복사할 데이터에 대한 포인터입니다. 바인딩된 데이터 형식이 큰 값 형식 (예: SQLTEXT 또는 SQLIMAGE) *pData* NULL 일 수 있습니다. NULL *pData* 청크를 사용 하 여 긴 데이터 값을 SQL Server로 전송 되지 않음을 나타내는 [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)합니다.  
  
 경우 *pData* NULL과 열으로 설정 된 큰 값 유형이 아닙니다 바인딩된 필드에 해당 하 **bcp_colptr** 실패 합니다.  
  
 큰 값 형식에 대 한 자세한 내용은 참조 하십시오. [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)**합니다.**  
  
 *idxServerCol*  
 데이터 복사 대상인 데이터베이스 테이블 열의 서수 위치입니다. 테이블의 첫 번째 열은 열 1입니다. 열의 서 수 위치를 보고 [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)합니다.  
  
## <a name="returns"></a>반환 값  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>주의  
 **bcp_colptr** 함수를 사용 하면 SQL server로 데이터를 복사할 때 특정 열에 대 한 원본 데이터의 주소를 변경할 수 있습니다 [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)합니다.  
  
 사용자 데이터에 대 한 포인터를 호출 하 여 초기에 설정 됩니다 **bcp_bind**합니다. 호출 간에 프로그램 변수 데이터 주소가 변경 되 면 **bcp_sendrow**를 호출할 수 있습니다 **bcp_colptr** 데이터에 포인터를 다시 설정 합니다. 다음 호출 **bcp_sendrow** 호출 하 여 주소가 지정 된 데이터를 보내는 **bcp_colptr**합니다.  
  
 별도 있어야 **bcp_colptr** 데이터 주소를 테이블의 모든 열에 대 한 호출을 수정 하려고 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [대량 복사 함수](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
