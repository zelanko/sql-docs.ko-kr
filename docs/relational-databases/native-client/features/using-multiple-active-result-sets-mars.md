---
title: MARS (Multiple Active Result Sets) 사용 | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, MARS
- SQLNCLI, MARS
- data access [SQL Server Native Client], MARS
- Multiple Active Result Sets
- SQL Server Native Client, MARS
- MARS [SQL Server]
- SQL Server Native Client ODBC driver, MARS
ms.assetid: ecfd9c6b-7d29-41d8-af2e-89d7fb9a1d83
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2b72f93aa979c504c0f6eeb6a3b867cc8360728f
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761307"
---
# <a name="using-multiple-active-result-sets-mars"></a>MARS(Multiple Active Result Sets) 사용

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]에 액세스하는 애플리케이션에서 MARS(Multiple Active Result Sets)를 지원합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 데이터베이스 애플리케이션이 연결에 대한 다중 활성 문을 유지할 수 없었습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기본 결과 집합을 사용할 경우 애플리케이션에서 한 일괄 작업의 모든 결과 집합을 처리하거나 취소해야만 해당 연결에서 다른 일괄 작업을 실행할 수 있었습니다. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서는 애플리케이션에서 연결당 둘 이상의 보류 중인 요청을 유지할 수 있도록 하는 새로운 연결 특성이 도입되었습니다. 즉, 연결당 둘 이상의 활성 기본 결과 집합을 유지할 수 있게 되었습니다.  
  
 MARS는 다음과 같은 새로운 기능을 사용하여 애플리케이션 디자인을 단순화합니다.  
  
-   애플리케이션에서 여러 기본 결과 집합을 열어 두고 읽기를 인터리브할 수 있습니다.  
  
-   애플리케이션이 기본 결과 집합을 연 상태로 다른 문(INSERT, UPDATE, DELETE 및 저장 프로시저 호출 등)을 실행할 수 있습니다.  
  
 다음은 MARS를 사용하는 애플리케이션에 유용한 지침입니다.  
  
-   단일 SQL 문(SELECT, OUTPUT이 있는 DML, RECEIVE, READ TEXT 등)으로 생성된 일시적으로 존재하거나 크기가 작은 결과 집합에 대해서는 기본 결과 집합을 사용해야 합니다.  
  
-   단일 SQL 문으로 생성된 오래 존재하거나 크기가 큰 결과 집합에 대해서는 서버 커서를 사용해야 합니다.  
  
-   결과 반환 여부에 관계없이 프로시저 관련 요청이나 다중 결과를 반환하는 일괄 처리에서는 항상 결과의 끝까지 읽어야 합니다.  
  
-   가능한 경우에는 항상 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문 대신 API 호출을 사용하여 연결 속성을 변경하고 트랜잭션을 관리해야 합니다.  
  
-   MARS에서 동시 일괄 처리가 실행되는 동안에는 세션 범위의 가장이 금지됩니다.  

> [!NOTE]
> 기본적으로 MARS 기능은 드라이버에서 사용 하도록 설정 되지 않습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 사용 하 여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결 하는 경우 MARS를 사용 하려면 연결 문자열 내에서 MARS를 특별히 사용 하도록 설정 해야 합니다. 그러나 응용 프로그램에서 드라이버가 MARS를 지원 한다는 것을 감지 하는 경우 일부 응용 프로그램은 기본적으로 MARS를 사용 하도록 설정할 수 있습니다. 이러한 응용 프로그램의 경우 필요에 따라 연결 문자열에서 MARS를 사용 하지 않도록 설정할 수 있습니다. 자세한 내용은 이 항목의 뒷부분에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 섹션을 참조하십시오.

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 연결에서 활성 문의 수를 제한하지 않습니다.  
  
 단일 다중 문 일괄 처리 또는 저장 프로시저를 동시에 실행 하지 않아도 되는 일반적인 응용 프로그램은 MARS 구현 방법을 이해 하지 않고도 MARS의 이점을 누릴 수 있습니다. 하지만 요구 사항이 복잡한 애플리케이션에서는 MARS 구현 방법을 고려해야 합니다.  
  
 MARS를 사용하면 단일 연결 내에서 여러 요청의 실행을 인터리브할 수 있습니다. 즉, 일괄 처리를 실행할 수 있으며 해당 일괄 처리가 실행되는 동안 요청을 실행할 수 있습니다. 하지만 MARS는 병렬 실행이 아니라 인터리브로 정의된다는 것에 주의하십시오.  
  
 MARS 인프라에서는 다중 일괄 처리를 인터리브 방식으로 실행할 수 있습니다. 하지만 실행은 잘 정의된 지점에서만 전환할 수 있습니다. 또한 대부분의 문은 일괄 처리 내에서 개별적으로 실행되어야 합니다. 클라이언트에 행을 반환 하는 문 (예: *생성 지점이*라고도 함)은 행이 클라이언트에 전송 되는 동안 완료 되기 전에 인터리브 실행이 허용 됩니다. 예를 들면 다음과 같습니다.  
  
-   SELECT  
  
-   FETCH  
  
-   RECEIVE  
  
 저장 프로시저나 일괄 처리의 일부로 실행되는 다른 모든 문은 실행이 완료된 후에만 다른 MARS 요청으로 실행을 전환할 수 있습니다.  
  
 일괄 처리에서 실행이 인터리브되는 세부적인 방식은 많은 요소의 영향을 받게 되므로 양보점을 포함하는 다중 일괄 처리에서 명령이 실행되는 정확한 순서를 예측하기 어렵습니다. 따라서 이와 같은 복잡한 일괄 처리의 인터리브 실행 때문에 원하지 않는 결과가 나타나지 않도록 주의하십시오.  
  
 연결 상태(SET, USE) 및 트랜잭션(BEGIN TRAN, COMMIT, ROLLBACK)을 관리하는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문 대신 API 호출을 사용하여 양보점을 포함할 수 있는 다중 문 일괄 처리에 이러한 문이 포함되지 않도록 하고 모든 결과를 사용하거나 취소하여 이러한 일괄 처리의 실행을 직렬화함으로써 문제를 방지합니다.  
  
> [!NOTE]  
>  MARS를 설정할 경우 수동 또는 암시적 트랜잭션을 시작하는 일괄 처리 또는 저장 프로시저는 트랜잭션을 완료한 후 일괄 처리를 종료해야 합니다. 그렇지 않으면 일괄 처리가 완료될 때 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 해당 트랜잭션으로 수행된 모든 변경 사항을 롤백합니다. 그와 같은 트랜잭션은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 일괄 처리 범위 트랜잭션으로 관리됩니다. 이것은 MARS를 설정할 경우 올바르게 동작하는 기존 저장 프로시저를 사용할 수 있도록 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에 새로 도입된 트랜잭션 형식입니다. 일괄 처리 범위 트랜잭션에 대 한 자세한 내용은 [Transaction 문 &#40;transact-sql&#41;](~/t-sql/statements/statements.md)을 참조 하세요.  
  
 ADO에서 MARS를 사용 하는 예제는 [SQL Server Native Client에서 Ado 사용](../../../relational-databases/native-client/applications/using-ado-with-sql-server-native-client.md)을 참조 하세요.  
  
## <a name="in-memory-oltp"></a>메모리 내 OLTP  
 메모리 내 OLTP는 쿼리 및 고유 하 게 컴파일된 저장 프로시저를 사용 하는 MARS를 지원 합니다. MARS를 사용 하면 새 결과 집합에서 행을 인출 하기 위해 요청을 보내기 전에 각 결과 집합을 완전히 검색할 필요 없이 여러 쿼리에서 데이터를 요청할 수 있습니다. 열려 있는 여러 결과 집합에서 성공적으로 읽으려면 MARS 사용 연결을 사용 해야 합니다.  
  
 MARS는 기본적으로 사용 되지 않으므로 연결 문자열에 `MultipleActiveResultSets=True`을 추가 하 여 명시적으로 사용 하도록 설정 해야 합니다. 다음 예에서는 SQL Server 인스턴스에 연결 하 고 MARS를 사용 하도록 지정 하는 방법을 보여 줍니다.  
  
```  
Data Source=MSSQL; Initial Catalog=AdventureWorks; Integrated Security=SSPI; MultipleActiveResultSets=True  
```  
  
 메모리 내 OLTP를 사용 하는 MARS는 기본적으로 나머지 SQL 엔진의 MARS와 동일 합니다. 다음은 메모리 최적화 테이블 및 고유 하 게 컴파일된 저장 프로시저에서 MARS를 사용 하는 경우의 차이점을 보여 줍니다.  
  
 **MARS 및 메모리 액세스에 최적화 된 테이블**  
  
 MARS 사용 연결을 사용 하는 경우 디스크 기반 테이블과 메모리 최적화 테이블 간의 차이점은 다음과 같습니다.  
  
-   두 문이 동일한 대상 개체의 데이터를 수정할 수 있지만 둘 다 동일한 레코드를 수정 하려고 하면 쓰기-쓰기 충돌이 발생 하 여 새 작업이 실패 합니다. 그러나 두 작업 모두 다른 레코드를 수정 하는 경우 작업이 성공 합니다.  
  
-   각 문은 스냅숏 격리에서 실행 되므로 새 작업에서 기존 문의 변경 내용을 볼 수 없습니다. 동시 문이 동일한 트랜잭션에서 실행 되는 경우에도 SQL 엔진은 서로 격리 된 각 문에 대해 일괄 처리 범위의 트랜잭션을 만듭니다. 그러나 일괄 처리 범위의 트랜잭션은 여전히 함께 바인딩되어 있으므로 하나의 일괄 처리 범위 트랜잭션의 롤백이 동일한 일괄 처리의 다른 일괄 처리에 영향을 줍니다.  
  
-   사용자 트랜잭션에서는 DDL 작업을 수행할 수 없으므로 즉시 오류가 발생 합니다.  
  
 **MARS 및 고유하게 컴파일된 저장 프로시저**  
  
 고유 하 게 컴파일된 저장 프로시저는 MARS를 사용 하는 연결에서 실행할 수 있으며 yield 점이 발견 될 때만 다른 문으로 실행 될 수 있습니다. Yield point에는 다른 문으로 실행을 양보할 수 있는 고유 하 게 컴파일된 저장 프로시저 내의 유일한 문인 SELECT 문이 필요 합니다. SELECT 문이 프로시저에 없으면 생성 되지 않으며 다른 문이 시작 되기 전에 완료 될 때까지 실행 됩니다.  
  
 **MARS 및 메모리 내 OLTP 트랜잭션**  
  
 인터리빙 된 문과 원자성 블록에서 변경한 내용은 서로 격리 됩니다. 예를 들어 한 문 또는 atomic 블록이 일부 변경 작업을 수행 하 고 다른 문으로 실행을 생성 하는 경우 새 문은 첫 번째 문에서 변경한 내용을 볼 수 없습니다. 또한 첫 번째 문이 실행을 다시 시작 하면 다른 문에서 변경한 내용이 표시 되지 않습니다. 문은 문이 시작 되기 전에 완료 되 고 커밋된 변경 내용만 표시 합니다.  
  
 BEGIN TRANSACTION 문을 사용 하 여 현재 사용자 트랜잭션 내에서 새 사용자 트랜잭션을 시작할 수 있습니다 .이는 interop 모드 에서만 지원 되므로 BEGIN TRANSACTION는 T-sql 문에서만 호출 될 수 있으며 고유 하 게 컴파일된 저장 된에서 사용할 수 없습니다. 여기서. 트랜잭션에 SAVE TRANSACTION 또는 API 호출을 사용 하 여 트랜잭션에 저장 점을 만들 수 있습니다. 저장 점으로 롤백하려면 (save_point_name)를 저장 합니다. 이 기능은 T-sql 문에서만 사용할 수 있으며 고유 하 게 컴파일된 저장 프로시저에서 사용할 수 없습니다.  
  
 **MARS 및 columnstore 인덱스**  
  
 SQL Server (2016부터)는 columnstore 인덱스를 사용 하는 MARS를 지원 합니다. SQL Server 2014는 MARS를 사용하여 columnstore 인덱스가 있는 테이블에 대한 읽기 전용 연결을 합니다.    그러나 SQL Server 2014는 columnstore 인덱스가 있는 테이블에서 DML(동시 데이터 조작 언어) 작업에 대해서는 MARS를 지원하지 않습니다. 이 경우 SQL Server는 연결을 종료하고 트랜잭션을 중단합니다.   SQL Server 2012에는 읽기 전용 columnstore 인덱스가 있으며 MARS에는 적용 되지 않습니다.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 공급자  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DBPROPSET_SQLSERVERDBINIT 속성 집합에서 구현 되는 SSPROP_INIT_MARSCONNECTION 데이터 원본 초기화 속성을 추가 하 여 MARS를 지원 합니다. 이와 함께 새 연결 문자열 키워드인 **MarsConn**이 추가되었습니다. **True** 또는 **false** 값을 허용 합니다. 기본값은 **false** 입니다.  
  
 데이터 원본 속성 DBPROP_MULTIPLECONNECTIONS의 기본값은 VARIANT_TRUE입니다. 이것은 공급자가 다중 동시 명령 및 행 집합 개체를 지원하기 위해 다중 연결을 생성한다는 의미입니다. MARS를 사용 하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 단일 연결에서 여러 명령 및 행 집합 개체를 지원할 수 있으므로 MULTIPLE_CONNECTIONS은 기본적으로 VARIANT_FALSE로 설정 됩니다.  
  
 DBPROPSET_SQLSERVERDBINIT 속성 집합의 향상 된 기능에 대 한 자세한 내용은 [초기화 및 권한 부여 속성](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)을 참조 하세요.  
  
### <a name="sql-server-native-client-ole-db-provider-example"></a>SQL Server Native Client OLE DB 공급자 예  
 이 예에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native OLE DB 공급자를 사용 하 여 데이터 원본 개체를 만들고, 세션 개체를 만들기 전에 DBPROPSET_SQLSERVERDBINIT 속성 집합을 사용 하 여 MARS를 사용 하도록 설정 합니다.  
  
```cpp
#include <sqlncli.h>  
  
IDBInitialize *pIDBInitialize = NULL;  
IDBCreateSession *pIDBCreateSession = NULL;  
IDBProperties *pIDBProperties = NULL;  
  
// Create the data source object.  
hr = CoCreateInstance(CLSID_SQLNCLI10, NULL,  
   CLSCTX_INPROC_SERVER,  
   IID_IDBInitialize,   
    (void**)&pIDBInitialize);  
  
hr = pIDBInitialize->QueryInterface(IID_IDBProperties, (void**)&pIDBProperties);  
  
// Set the MARS property.  
DBPROP rgPropMARS;  
  
// The following is necessary since MARS is off by default.  
rgPropMARS.dwPropertyID = SSPROP_INIT_MARSCONNECTION;  
rgPropMARS.dwOptions = DBPROPOPTIONS_REQUIRED;  
rgPropMARS.dwStatus = DBPROPSTATUS_OK;  
rgPropMARS.colid = DB_NULLID;  
V_VT(&(rgPropMARS.vValue)) = VT_BOOL;  
V_BOOL(&(rgPropMARS.vValue)) = VARIANT_TRUE;  
  
// Create the structure containing the properties.  
DBPROPSET PropSet;  
PropSet.rgProperties = &rgPropMARS;  
PropSet.cProperties = 1;  
PropSet.guidPropertySet = DBPROPSET_SQLSERVERDBINIT;  
  
// Get an IDBProperties pointer and set the initialization properties.  
pIDBProperties->SetProperties(1, &PropSet);  
pIDBProperties->Release();  
  
// Initialize the data source object.  
hr = pIDBInitialize->Initialize();  
  
//Create a session object from a data source object.  
IOpenRowset * pIOpenRowset = NULL;  
hr = IDBInitialize->QueryInterface(IID_IDBCreateSession, (void**)&pIDBCreateSession));  
hr = pIDBCreateSession->CreateSession(  
   NULL,             // pUnkOuter  
   IID_IOpenRowset,  // riid  
  &pIOpenRowset ));  // ppSession  
  
// Create a rowset with a firehose mode cursor.  
IRowset *pIRowset = NULL;  
DBPROP rgRowsetProperties[2];  
  
// To get a firehose mode cursor request a   
// forward only read only rowset.  
rgRowsetProperties[0].dwPropertyID = DBPROP_IRowsetLocate;  
rgRowsetProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
rgRowsetProperties[0].dwStatus = DBPROPSTATUS_OK;  
rgRowsetProperties[0].colid = DB_NULLID;  
VariantInit(&(rgRowsetProperties[0].vValue));  
rgRowsetProperties[0].vValue.vt = VARIANT_BOOL;  
rgRowsetProperties[0].vValue.boolVal = VARIANT_FALSE;  
  
rgRowsetProperties[1].dwPropertyID = DBPROP_IRowsetChange;  
rgRowsetProperties[1].dwOptions = DBPROPOPTIONS_REQUIRED;  
rgRowsetProperties[1].dwStatus = DBPROPSTATUS_OK;  
rgRowsetProperties[1].colid = DB_NULLID;  
VariantInit(&(rgRowsetProperties[1].vValue));  
rgRowsetProperties[1].vValue.vt = VARIANT_BOOL;  
rgRowsetProperties[1].vValue.boolVal = VARIANT_FALSE;  
  
DBPROPSET rgRowsetPropSet[1];  
rgRowsetPropSet[0].rgProperties = rgRowsetProperties  
rgRowsetPropSet[0].cProperties = 2  
rgRowsetPropSet[0].guidPropertySet = DBPROPSET_ROWSET;  
  
hr = pIOpenRowset->OpenRowset (NULL,  
   &TableID,  
   NULL,  
   IID_IRowset,  
   1,  
   rgRowsetPropSet  
   (IUnknown**)&pIRowset);  
```  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 드라이버  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 및 [SQLGetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) 함수를 추가 하 여 MARS를 지원 합니다. SQL_MARS_ENABLED_YES 또는 SQL_MARS_ENABLED_NO를 받아들이는 SQL_COPT_SS_MARS_ENABLED가 추가되었으며 기본값은 SQL_MARS_ENABLED_NO입니다. 또한 새 연결 문자열 키워드인 **Mars_Connection**추가 되었습니다. 이 키워드는 "yes" 또는 "no" 값을 받으며, 기본값은 "no"입니다.  
  
### <a name="sql-server-native-client-odbc-driver-example"></a>SQL Server Native Client ODBC 드라이버 예  
 이 예에서는 **SQLDriverConnect** 함수를 호출 하 여 데이터베이스를 연결 하기 전에 **SQLSetConnectAttr** 함수를 사용 하 여 MARS를 설정 합니다. 연결이 설정 되 면 두 개의 **Sqlexecdirect** 함수를 호출 하 여 동일한 연결에서 두 개의 별도 결과 집합을 만듭니다.  
  
```cpp
#include <sqlncli.h>  
  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_MARS_ENABLED, SQL_MARS_ENABLED_YES, SQL_IS_UINTEGER);  
SQLDriverConnect(hdbc, hwnd,   
   "DRIVER=SQL Server Native Client 10.0;  
   SERVER=(local);trusted_connection=yes;", SQL_NTS, szOutConn,   
   MAX_CONN_OUT, &cbOutConn, SQL_DRIVER_COMPLETE);  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt1);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt2);  
  
// The 2nd execute would have failed with connection busy error if  
// MARS were not enabled.  
SQLExecDirect(hstmt1, L"SELECT * FROM Authors", SQL_NTS);  
SQLExecDirect(hstmt2, L"SELECT * FROM Titles", SQL_NTS);  
  
// Result set processing can interleave.  
SQLFetch(hstmt1);  
SQLFetch(hstmt2);  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Native Client 기능](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [SQL Server 기본 결과 집합 사용](../../../relational-databases/native-client-odbc-cursors/implementation/using-sql-server-default-result-sets.md)  
  
  
