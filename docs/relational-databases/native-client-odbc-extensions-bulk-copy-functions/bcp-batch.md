---
title: bcp_batch | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_batch
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_batch function
ms.assetid: 0bda489e-86bc-4a7e-80f6-96047e03f281
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f435b0ba0d7474867af20aea1d59bd6118035623
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73783236"
---
# <a name="bcp_batch"></a>bcp_batch
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  이전에 프로그램 변수에서 대량 복사하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bcp_sendrow [를 사용하여](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)로 보낸 행을 모두 커밋합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DBINT bcp_batch (HDBC  
        hdbc);  
```  
  
## <a name="arguments"></a>인수  
 *hdbc*  
 대량 복사가 가능한 ODBC 연결 핸들입니다.  
  
## <a name="returns"></a>반환  
 
  **bcp_batch**를 마지막으로 호출한 후 저장된 행의 수입니다. 또는 오류가 발생하는 경우 -1입니다.  
  
## <a name="remarks"></a>설명  
 대량 복사 일괄 처리에서 트랜잭션을 정의합니다. 애플리케이션에서 [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) 및 **bcp_sendrow** 를 사용하여 프로그램 변수에서 SQL Server 테이블로 행을 대량 복사할 때 프로그램에서 **bcp_batch** 또는 [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md)을 호출할 경우에만 행이 커밋됩니다.  
  
 
  **bcp_batch** 는 *n* 번째 행마다 한 번씩 호출하거나 원격 계측 애플리케이션에서처럼 들어오는 데이터에 소강 상태가 있는 경우에 호출할 수 있습니다. 애플리케이션에서 **bcp_batch** 를 호출하지 않는 경우에는 **bcp_done** 을 호출할 때만 대량 복사된 행이 커밋됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Bulk Copy Functions](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
