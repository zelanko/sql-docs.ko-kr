---
title: "대량 복사 일괄 처리 크기 관리 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, bulk copy
- ODBC, bulk copy operations
- batches [ODBC]
- bulk copy [ODBC], batch sizes
ms.assetid: 4b24139f-788b-45a6-86dc-ae835435d737
caps.latest.revision: "32"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ff6ef76f4cd59d845f95f17e8b072dc1311052f4
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="managing-bulk-copy-batch-sizes"></a>대량 복사 일괄 처리 크기 관리
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  대량 복사 작업에서 일괄 처리의 주요 목적은 트랜잭션의 범위를 정의하는 것입니다. 일괄 처리 크기를 설정하지 않으면 대량 복사 함수에서 전체 대량 복사를 하나의 트랜잭션으로 간주합니다. 일괄 처리 크기를 설정하면 각 일괄 처리에서 일괄 처리가 완료될 때 커밋되는 하나의 트랜잭션이 구성됩니다.  
  
 일괄 처리 크기를 지정하지 않고 대량 복사를 수행하는 동안 오류가 발생하면 전체 대량 복사가 롤백됩니다. 장기 실행 대량 복사는 복구하는 데 오랜 시간이 걸릴 수 있습니다. 일괄 처리 크기를 설정하면 대량 복사에서 각 일괄 처리를 하나의 트랜잭션으로 간주하고 각 일괄 처리를 커밋합니다. 오류가 발생할 경우 처리 중인 마지막 일괄 작업만 롤백되면 됩니다.  
  
 일괄 처리 크기는 잠금 오버헤드에도 영향을 줄 수 있습니다. 에 대 한 대량 복사를 수행할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], TABLOCK 힌트를 사용 하 여 지정할 수 있습니다 [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) 행 잠금 대신 테이블 잠금을 획득 하려고 합니다. 오버헤드를 최소화하여 전체 대량 복사 작업에 대해 단일 테이블 잠금을 보유할 수 있습니다. TABLOCK을 지정하지 않으면 개별 행에 잠금이 설정되고, 대량 복사 기간 동안 모든 잠금을 유지 관리하는 오버헤드로 인해 성능이 느려질 수 있습니다. 트랜잭션 기간 동안에만 잠금이 보유되므로 일괄 처리 크기를 지정하면 현재 보유된 잠금을 해제하는 커밋이 정기적으로 생성되어 이 문제가 해결됩니다.  
  
 많은 행을 대량 복사하는 경우 일괄 처리를 구성하는 행 수가 성능에 큰 영향을 줄 수 있습니다. 권장되는 일괄 처리 크기는 수행하는 대량 복사 유형에 따라 달라집니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 대량 복사하는 경우 TABLOCK 대량 복사 힌트를 지정하고 큰 일괄 처리 크기를 설정합니다.  
  
-   TABLOCK이 지정되지 않은 경우 일괄 처리 크기를 1,000행 미만으로 제한합니다.  
  
 호출 하 여 일괄 처리 크기 지정 대량 데이터 파일에서 복사 하는 경우 **bcp_control** 호출 하기 전에 BCPBATCH 옵션으로 [bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md)합니다. 대량 복사를 사용 하 여 프로그램 변수에서 하는 경우 [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) 및 [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)를 호출 하 여 일괄 처리 크기를 제어 [bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md) 호출한 후 [bcp_ sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) *x* 시간, where *x* 일괄 처리의 행 수입니다.  
  
 트랜잭션 크기를 지정하는 것 외에도 일괄 처리는 행이 네트워크를 통해 서버로 전송되는 시기에 영향을 줍니다. 대량 복사 함수에서 행을 일반적으로 캐시 **bcp_sendrow** 때까지 네트워크 패킷을, 다음 찬 패킷을 서버로 보냅니다. 그러나 응용 프로그램 호출 하는 경우 **bcp_batch**, 현재 패킷이 채워 졌가 있는지 여부에 관계 없이 서버에 전송 됩니다. 매우 작은 일괄 처리 크기를 사용하면 부분적으로 채워진 많은 패킷이 서버로 전송되므로 성능이 느려질 수 있습니다. 예를 들어 호출 **bcp_batch** 후 모든 **bcp_sendrow** 하면 각 행이 개별 패킷으로 전송 하 고 행이 매우 큰, 하지 않으면 각 패킷의 공간이 낭비 됩니다. SQL Server에 대 한 네트워크 패킷의 기본 크기는 4KB 이며 응용 프로그램 호출 하 여 크기를 변경할 수는 있지만 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) SQL_ATTR_PACKET_SIZE 특성을 지정 합니다.  
  
 일괄 처리의 또 다른 부작용은 각 일괄 처리로 완료 될 때까지 설정 처리 중인 결과 것으로 간주 됩니다 **bcp_batch**합니다. 보고서를 일괄 처리는 보류 중인 동안 연결 핸들에서 다른 작업을 시도한 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 sqlstate 오류가 발생 = "HY000" 및 오류 메시지 문자열입니다.  
  
```  
"[Microsoft][SQL Server Native Client] Connection is busy with  
results for another hstmt."  
```  
  
## <a name="see-also"></a>관련 항목:  
 [수행 하는 대량 복사 작업 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)   
 [데이터 대량 가져오기 및 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)  
  
  
