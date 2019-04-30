---
title: 스냅숏 격리 작업 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], snapshot isolation
- SQLNCLI, snapshot isolation
- isolation levels [SQL Server], snapshot
- DBPROPSET_SESSION property set
- DBDROPSET_DATASOURCEINFO property set
- snapshot isolation [SQL Server Native Client]
- SQL Server Native Client OLE DB provider, snapshot isolation
- SQL Server Native Client ODBC driver, snapshot isolation
- SQL Server Native Client, snapshot isolation
- SQLGetInfo function
- concurrency [SQL Server Native Client]
- SQLSetConnectAttr function
ms.assetid: 39e87eb1-677e-45dd-bc61-83a4025a7756
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dcf2003873de6f6ca15fed4d0818337ce4920906
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63205860"
---
# <a name="working-with-snapshot-isolation"></a>스냅숏 격리 작업
  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서는 OLTP(온라인 트랜잭션 처리) 응용 프로그램의 동시성을 향상시키기 위한 새로운 "스냅숏" 격리 수준이 도입되었습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 동시성이 일부 응용 프로그램에 대해 문제 차단 및 교착 상태를 발생시킬 수 있는 잠금 기능에만 의존했습니다. 스냅숏 격리는 향상된 행 버전 관리 기능을 사용하며 읽기/쓰기 차단 시나리오를 방지하여 성능을 향상시킵니다.  
  
 스냅숏 격리 하에 시작된 트랜잭션은 트랜잭션이 시작된 시간을 기준으로 데이터베이스 스냅숏을 읽습니다. 그 결과, 스냅숏 트랜잭션 컨텍스트 내에서 열린 키 집합 동적 및 정적 서버 커서가 직렬화 가능 트랜잭션 내에서 열린 정적 커서처럼 동작합니다. 하지만 스냅숏 격리 수준 하에서 커서를 열면 잠금이 수행되지 않아 서버의 차단을 줄일 수 있습니다.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 공급자  
 합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에 도입 된 스냅숏 격리를 활용 하는 향상 된 기능에 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]입니다. 이러한 향상된 기능에는 DATASOURCEINFO 및 DBPROPSET_SESSION 속성 집합의 변경 내용이 포함됩니다.  
  
### <a name="dbpropsetdatasourceinfo"></a>DBPROPSET_DATASOURCEINFO  
 DBPROPSET_DATASOURCEINFO 속성 집합은 DBPROP_SUPPORTEDTXNISOLEVELS 속성에 사용되는 DBPROPVAL_TI_SNAPSHOT 값을 추가하여 스냅숏 격리가 지원됨을 나타내도록 변경되었습니다. 이 새로운 값은 데이터베이스에 버전 관리가 설정되어 있는지 여부에 관계없이 스냅숏 격리가 지원됨을 나타냅니다. 다음은 DBPROP_SUPPORTEDTXNISOLEVELS 값의 목록입니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|DBPROP_SUPPORTEDTXNISOLEVELS|형식: VT_I4<br /><br /> R/W: 읽기 전용<br /><br /> 설명: 지원 되는 트랜잭션 격리 수준을 지정 하는 비트 마스크입니다. 다음을 0개 이상 조합하여 지정합니다.<br /><br /> -   DBPROPVAL_TI_CHAOS<br />-   DBPROPVAL_TI_READUNCOMMITTED<br />-   DBPROPVAL_TI_BROWSE<br />-   DBPROPVAL_TI_CURSORSTABILITY<br />-   DBPROPVAL_TI_READCOMMITTED<br />-   DBPROPVAL_TI_REPEATABLEREAD<br />-   DBPROPVAL_TI_SERIALIZABLE<br />-   DBPROPVAL_TI_ISOLATED<br />-   DBPROPVAL_TI_SNAPSHOT|  
  
### <a name="dbpropsetsession"></a>DBPROPSET_SESSION  
 DBPROPSET_SESSION 속성 집합은 DBPROP_SESS_AUTOCOMMITISOLEVELS 속성에 사용되는 DBPROPVAL_TI_SNAPSHOT 값을 추가하여 스냅숏 격리가 지원됨을 나타내도록 변경되었습니다. 이 새로운 값은 데이터베이스에 버전 관리가 설정되어 있는지 여부에 관계없이 스냅숏 격리가 지원됨을 나타냅니다. 다음은 DBPROP_SESS_AUTOCOMMITISOLEVELS 값의 목록입니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|형식: VT_I4<br /><br /> R/W: 읽기 전용<br /><br /> 설명: 자동 커밋 모드에서는 트랜잭션 격리 수준을 나타내는 비트 마스크를 지정 합니다. 이 비트 마스크에 설정할 수 있는 값은 DBPROP_SUPPORTEDTXNISOLEVELS에 설정할 수 있는 값과 같습니다.|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]보다 이전 버전의 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]를 사용할 때 DBPROPVAL_TI_SNAPSHOT을 설정하면 오류 DB_S_ERRORSOCCURRED 또는 DB_E_ERRORSOCCURRED가 발생합니다.  
  
 스냅숏 격리 트랜잭션에서 지원 되는 방법에 대 한 자세한 내용은 [로컬 트랜잭션을 지원](../../native-client-ole-db-transactions/transactions.md)합니다.  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 드라이버  
 합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 지원 스냅숏 격리 하지만 향상 된 [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) 및 [SQLGetInfo](../../native-client-odbc-api/sqlgetinfo.md) 함수입니다.  
  
### <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 합니다 **SQLSetConnectAttr** 함수는 이제 SQL_COPT_SS_TXN_ISOLATION 특성 사용을 지원 합니다. SQL_COPT_SS_TXN_ISOLATION을 SQL_TXN_SS_SNAPSHOT으로 설정하면 스냅숏 격리 수준에서 트랜잭션이 실행됩니다.  
  
### <a name="sqlgetinfo"></a>SQLGetInfo  
 합니다 [SQLGetInfo](../../native-client-odbc-api/sqlgetinfo.md) 함수에는 이제에서 SQL_TXN_ISOLATION_OPTION 정보 유형에 추가 된 SQL_TXN_SS_SNAPSHOT 값을 지원 합니다.  
  
 스냅숏 격리 트랜잭션에서 지원 되는 방법에 대 한 자세한 내용은 [커서 트랜잭션 격리 수준](../../native-client-odbc-cursors/properties/cursor-transaction-isolation-level.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client 기능](sql-server-native-client-features.md)   
 [행 집합 속성 및 동작](../../native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
  
