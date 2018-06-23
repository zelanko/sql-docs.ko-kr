---
title: 스냅숏 격리 작업 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
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
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 97280da27703892a916827bdcd6f31a327fbc360
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35698514"
---
# <a name="working-with-snapshot-isolation"></a>스냅숏 격리 작업
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서는 OLTP(온라인 트랜잭션 처리) 응용 프로그램의 동시성을 향상시키기 위한 새로운 "스냅숏" 격리 수준이 도입되었습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 동시성이 일부 응용 프로그램에 대해 문제 차단 및 교착 상태를 발생시킬 수 있는 잠금 기능에만 의존했습니다. 스냅숏 격리는 향상된 행 버전 관리 기능을 사용하며 읽기/쓰기 차단 시나리오를 방지하여 성능을 향상시킵니다.  
  
 스냅숏 격리 하에 시작된 트랜잭션은 트랜잭션이 시작된 시간을 기준으로 데이터베이스 스냅숏을 읽습니다. 그 결과, 스냅숏 트랜잭션 컨텍스트 내에서 열린 키 집합 동적 및 정적 서버 커서가 직렬화 가능 트랜잭션 내에서 열린 정적 커서처럼 동작합니다. 하지만 스냅숏 격리 수준 하에서 커서를 열면 잠금이 수행되지 않아 서버의 차단을 줄일 수 있습니다.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 공급자  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에 도입 된 스냅숏 격리를 활용 하는 향상 된 기능에 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]합니다. 이러한 향상된 기능에는 DATASOURCEINFO 및 DBPROPSET_SESSION 속성 집합의 변경 내용이 포함됩니다.  
  
### <a name="dbpropsetdatasourceinfo"></a>DBPROPSET_DATASOURCEINFO  
 DBPROPSET_DATASOURCEINFO 속성 집합은 DBPROP_SUPPORTEDTXNISOLEVELS 속성에 사용되는 DBPROPVAL_TI_SNAPSHOT 값을 추가하여 스냅숏 격리가 지원됨을 나타내도록 변경되었습니다. 이 새로운 값은 데이터베이스에 버전 관리가 설정되어 있는지 여부에 관계없이 스냅숏 격리가 지원됨을 나타냅니다. 다음은 DBPROP_SUPPORTEDTXNISOLEVELS 값의 목록입니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|DBPROP_SUPPORTEDTXNISOLEVELS|형식: VT_I4<br /><br /> R/w: 읽기 전용<br /><br /> 에 대 한 비트 마스크 지원 되는 트랜잭션 격리 수준을 지정 하는입니다. 다음을 0개 이상 조합하여 지정합니다.<br /><br /> DBPROPVAL_TI_CHAOS<br /><br /> DBPROPVAL_TI_READUNCOMMITTED<br /><br /> DBPROPVAL_TI_BROWSE<br /><br /> DBPROPVAL_TI_CURSORSTABILITY<br /><br /> DBPROPVAL_TI_READCOMMITTED<br /><br /> DBPROPVAL_TI_REPEATABLEREAD<br /><br /> DBPROPVAL_TI_SERIALIZABLE<br /><br /> DBPROPVAL_TI_ISOLATED<br /><br /> DBPROPVAL_TI_SNAPSHOT|  
  
### <a name="dbpropsetsession"></a>DBPROPSET_SESSION  
 DBPROPSET_SESSION 속성 집합은 DBPROP_SESS_AUTOCOMMITISOLEVELS 속성에 사용되는 DBPROPVAL_TI_SNAPSHOT 값을 추가하여 스냅숏 격리가 지원됨을 나타내도록 변경되었습니다. 이 새로운 값은 데이터베이스에 버전 관리가 설정되어 있는지 여부에 관계없이 스냅숏 격리가 지원됨을 나타냅니다. 다음은 DBPROP_SESS_AUTOCOMMITISOLEVELS 값의 목록입니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|형식: VT_I4<br /><br /> R/w: 읽기 전용<br /><br /> 설명: 자동 커밋 모드에서는 트랜잭션 격리 수준을 나타내는 비트 마스크를 지정 합니다. 이 비트 마스크에 설정할 수 있는 값은 DBPROP_SUPPORTEDTXNISOLEVELS에 설정할 수 있는 값과 같습니다.|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]보다 이전 버전의 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]를 사용할 때 DBPROPVAL_TI_SNAPSHOT을 설정하면 오류 DB_S_ERRORSOCCURRED 또는 DB_E_ERRORSOCCURRED가 발생합니다.  
  
 스냅숏 격리 트랜잭션에서 지원 되는 방법에 대 한 정보를 참조 하십시오. [로컬 트랜잭션 지원](../../../relational-databases/native-client-ole-db-transactions/supporting-local-transactions.md)합니다.  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 드라이버  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 지원 스냅숏 격리에 대 한 하지만 향상 된 [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 및 [SQLGetInfo](../../../relational-databases/native-client-odbc-api/sqlgetinfo.md) 함수입니다.  
  
### <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 **SQLSetConnectAttr** 함수는 이제 SQL_COPT_SS_TXN_ISOLATION 특성의 사용을 지원 합니다. SQL_COPT_SS_TXN_ISOLATION을 SQL_TXN_SS_SNAPSHOT으로 설정하면 스냅숏 격리 수준에서 트랜잭션이 실행됩니다.  
  
### <a name="sqlgetinfo"></a>SQLGetInfo  
 [SQLGetInfo](../../../relational-databases/native-client-odbc-api/sqlgetinfo.md) 이제 함수에서 SQL_TXN_ISOLATION_OPTION 정보 유형에 추가 된 SQL_TXN_SS_SNAPSHOT 값을 지원 합니다.  
  
 스냅숏 격리 트랜잭션에서 지원 되는 방법에 대 한 정보를 참조 하십시오. [커서 트랜잭션 격리 수준을](../../../relational-databases/native-client-odbc-cursors/properties/cursor-transaction-isolation-level.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client 기능](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [행 집합 속성 및 동작](../../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
  
