---
title: bcp_sendrow | Microsoft Docs
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
apiname: bcp_sendrow
apilocation: sqlncli11.dll
apitype: DLLExport
helpviewer_keywords: bcp_sendrow function
ms.assetid: ddbdb4bd-ad4e-4bf1-9a75-656aa26ce10a
caps.latest.revision: "33"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d4312fedbd01082501faec1efd89a2cb1cd5161e
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="bcpsendrow"></a>bcp_sendrow
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  프로그램 변수에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 데이터 행을 보냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE bcp_sendrow (  
    HDBC hdbc);  
```  
  
## <a name="arguments"></a>인수  
 *hdbc*  
 대량 복사가 가능한 ODBC 연결 핸들입니다.  
  
## <a name="returns"></a>반환 값  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>주의  
 **bcp_sendrow** 함수 프로그램 변수에서 행을 작성 하 고에 보냅니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 호출 하기 전에 **bcp_sendrow**, 호출을 수행 해야 [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) 행 데이터를 포함 하는 프로그램 변수를 지정할 수 있습니다.  
  
 경우 **bcp_bind** 예를 들어 긴 가변 길이 데이터 형식 지정 이라고는 *eDataType* SQLTEXT 및 NULL이 아닌 매개 변수 *pData* 매개 변수, **bcp_sendrow** 와 같이 다른 데이터 형식에 대 한 전체 데이터 값을 보냅니다. 그러나 If, **bcp_bind** 에 NULL *pData* 매개 변수를 **bcp_sendrow** 지정 된 데이터가 있는 모든 열을 보낸 후에 즉시 응용 프로그램에 컨트롤 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 응용 프로그램이 호출할 수 [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) 반복적으로 하는 긴 가변 길이 데이터를 보내도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 한 번에 청크 합니다. 자세한 내용은 참조 [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)합니다.  
  
 때 **bcp_sendrow** 행을 대량 복사 프로그램 변수에서 데 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블, 행이 커밋됩니다 사용자를 호출 하는 경우에 [bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md) 또는 [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md) . 사용자를 호출 하도록 선택할 수 **bcp_batch** 되 면 모든  *n*  행 하거나 데이터가 연이어 사이의 소강 상태가 있는 때입니다. 경우 **bcp_batch** 은 호출 되지 행이 커밋됩니다 때 **bcp_done** 호출 됩니다.  
  
 대량 복사부터의 변경 내용은 주요에 대 한 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], 참조 [대량 복사 작업 수행 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [대량 복사 함수](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
