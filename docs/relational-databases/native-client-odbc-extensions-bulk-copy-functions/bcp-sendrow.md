---
description: bcp_sendrow
title: bcp_sendrow | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_sendrow
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_sendrow function
ms.assetid: ddbdb4bd-ad4e-4bf1-9a75-656aa26ce10a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c470244b1a739b989b5bcff36e8d0804b464bb4a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97483294"
---
# <a name="bcp_sendrow"></a>bcp_sendrow
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  프로그램 변수에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 데이터 행을 보냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RETCODE bcp_sendrow (  
    HDBC hdbc);  
```  
  
## <a name="arguments"></a>인수  
 *hdbc*  
 대량 복사가 가능한 ODBC 연결 핸들입니다.  
  
## <a name="returns"></a>반환  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>설명  
 **Bcp_sendrow** 함수는 프로그램 변수에서 행을 빌드하고로 보냅니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Bcp_sendrow** 를 호출 하기 전에 [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) 를 호출 하 여 행 데이터가 포함 된 프로그램 변수를 지정 해야 합니다.  
  
 Long, 가변 길이 데이터 형식 (예: SQLTEXT의 *Edatatype* 매개 변수 및 NULL이 아닌 *.pdata* 매개 변수)을 지정 하는 **bcp_bind** 를 호출 하면 **bcp_sendrow** 는 다른 데이터 형식과 마찬가지로 전체 데이터 값을 보냅니다. 그러나 **bcp_bind** 에 NULL *.pdata* 매개 변수가 있는 경우에는 지정 된 데이터가 있는 모든 열이로 전송 되는 즉시 응용 프로그램에 제어를 반환 **bcp_sendrow** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 그런 다음 응용 프로그램은 [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) 를 반복적으로 호출 하 여 긴 가변 길이 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 한 번에 청크로 보낼 수 있습니다. 자세한 내용은 [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)를 참조 하세요.  
  
 **Bcp_sendrow** 를 사용 하 여 프로그램 변수에서 테이블로 행을 대량 복사 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자가 [bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md) 또는 [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md)를 호출 하는 경우에만 행이 커밋됩니다. 사용자는 *n 개* 행 마다 또는 들어오는 데이터 기간 사이에 소강 상태가이 있는 경우 **bcp_batch** 를 호출 하도록 선택할 수 있습니다. **Bcp_batch** 를 호출 하지 않으면 **bcp_done** 를 호출할 때 행이 커밋됩니다.  
  
 에서 시작 하는 대량 복사의 주요 변경 내용에 대 한 자세한 내용은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [ODBC&#41;&#40;대량 복사 작업 수행 ](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Bulk Copy Functions](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
