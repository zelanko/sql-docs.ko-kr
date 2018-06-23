---
title: Multiple Active Result Sets MARS ()를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 52
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9f647aefd74f57c0c703fadd6e6a4179750bbfc4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092405"
---
# <a name="using-multiple-active-result-sets-mars"></a>MARS(Multiple Active Result Sets) 사용
  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 에 액세스 하는 응용 프로그램에서 여러 활성 결과 집합은 (MARS)에 대 한 지원 도입는 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 데이터베이스 응용 프로그램이 연결에 대한 다중 활성 문을 유지할 수 없었습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기본 결과 집합을 사용할 경우 응용 프로그램에서 한 일괄 작업의 모든 결과 집합을 처리하거나 취소해야만 해당 연결에서 다른 일괄 작업을 실행할 수 있었습니다. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서는 응용 프로그램에서 연결당 둘 이상의 보류 중인 요청을 유지할 수 있도록 하는 새로운 연결 특성이 도입되었습니다. 즉, 연결당 둘 이상의 활성 기본 결과 집합을 유지할 수 있게 되었습니다.  
  
 MARS는 다음과 같은 새로운 기능을 사용하여 응용 프로그램 디자인을 단순화합니다.  
  
-   응용 프로그램에서 여러 기본 결과 집합을 열어 두고 읽기를 인터리브할 수 있습니다.  
  
-   응용 프로그램이 기본 결과 집합을 연 상태로 다른 문(INSERT, UPDATE, DELETE 및 저장 프로시저 호출 등)을 실행할 수 있습니다.  
  
 다음은 MARS를 사용하는 응용 프로그램에 유용한 지침입니다.  
  
-   단일 SQL 문(SELECT, OUTPUT이 있는 DML, RECEIVE, READ TEXT 등)으로 생성된 일시적으로 존재하거나 크기가 작은 결과 집합에 대해서는 기본 결과 집합을 사용해야 합니다.  
  
-   단일 SQL 문으로 생성된 오래 존재하거나 크기가 큰 결과 집합에 대해서는 서버 커서를 사용해야 합니다.  
  
-   결과 반환 여부에 관계없이 프로시저 관련 요청이나 다중 결과를 반환하는 일괄 처리에서는 항상 결과의 끝까지 읽어야 합니다.  
  
-   가능한 경우에는 항상 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문 대신 API 호출을 사용하여 연결 속성을 변경하고 트랜잭션을 관리해야 합니다.  
  
-   MARS에서 동시 일괄 처리가 실행되는 동안에는 세션 범위의 가장이 금지됩니다.  
  
> [!NOTE]  
>  기본적으로 MARS 기능은 설정되어 있지 않습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 사용하여 연결할 때 MARS를 사용하려면 연결 문자열 내에서 명확하게 MARS를 설정해야 합니다. 자세한 내용은 이 항목의 뒷부분에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 섹션을 참조하십시오.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 연결에서 활성 문의 수를 제한하지 않습니다.  
  
 여러 개의 다중 문 일괄 처리가 필요 없거나 저장 프로시저를 동시에 실행할 필요가 없는 일반적인 응용 프로그램의 경우에는 MARS 구현 방법을 몰라도 MARS를 활용할 수 있습니다. 하지만 요구 사항이 복잡한 응용 프로그램에서는 MARS 구현 방법을 고려해야 합니다.  
  
 MARS를 사용하면 단일 연결 내에서 여러 요청의 실행을 인터리브할 수 있습니다. 즉, 일괄 처리를 실행할 수 있으며 해당 일괄 처리가 실행되는 동안 요청을 실행할 수 있습니다. 하지만 MARS는 병렬 실행이 아니라 인터리브로 정의된다는 것에 주의하십시오.  
  
 MARS 인프라에서는 다중 일괄 처리를 인터리브 방식으로 실행할 수 있습니다. 하지만 실행은 잘 정의된 지점에서만 전환할 수 있습니다. 또한 대부분의 문은 일괄 처리 내에서 개별적으로 실행되어야 합니다. 때때로 이라고 하는 클라이언트에 행을 반환 하는 문 *포인트를 생성*, 예를 들어 클라이언트에 전송 되 고 행 완료 되기 전에 실행을 인터리브할 수 있습니다.  
  
-   SELECT  
  
-   FETCH  
  
-   RECEIVE  
  
 저장 프로시저나 일괄 처리의 일부로 실행되는 다른 모든 문은 실행이 완료된 후에만 다른 MARS 요청으로 실행을 전환할 수 있습니다.  
  
 일괄 처리에서 실행이 인터리브되는 세부적인 방식은 많은 요소의 영향을 받게 되므로 양보점을 포함하는 다중 일괄 처리에서 명령이 실행되는 정확한 순서를 예측하기 어렵습니다. 따라서 이와 같은 복잡한 일괄 처리의 인터리브 실행 때문에 원하지 않는 결과가 나타나지 않도록 주의하십시오.  
  
 연결 상태(SET, USE) 및 트랜잭션(BEGIN TRAN, COMMIT, ROLLBACK)을 관리하는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문 대신 API 호출을 사용하여 양보점을 포함할 수 있는 다중 문 일괄 처리에 이러한 문이 포함되지 않도록 하고 모든 결과를 사용하거나 취소하여 이러한 일괄 처리의 실행을 직렬화함으로써 문제를 방지합니다.  
  
> [!NOTE]  
>  MARS를 설정할 경우 수동 또는 암시적 트랜잭션을 시작하는 일괄 처리 또는 저장 프로시저는 트랜잭션을 완료한 후 일괄 처리를 종료해야 합니다. 그렇지 않으면 일괄 처리가 완료될 때 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 해당 트랜잭션으로 수행된 모든 변경 사항을 롤백합니다. 그와 같은 트랜잭션은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 일괄 처리 범위 트랜잭션으로 관리됩니다. 이것은 MARS를 설정할 경우 올바르게 동작하는 기존 저장 프로시저를 사용할 수 있도록 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에 새로 도입된 트랜잭션 형식입니다. 일괄 처리 범위 트랜잭션에 대 한 자세한 내용은 참조 [Transaction 문을 &#40;TRANSACT-SQL&#41;](/sql/t-sql/language-elements/transactions-transact-sql)합니다.  
  
 ADO의 MARS를 사용 하 여 예제를 보려면 [SQL Server Native Client를 사용 하 여 ADO를 사용 하 여](../applications/using-ado-with-sql-server-native-client.md)합니다.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 공급자  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DBPROPSET_SQLSERVERDBINIT 속성 집합에 구현 된 SSPROP_INIT_MARSCONNECTION 데이터 원본 초기화 속성의 추가 통해 MARS를 지원 합니다. 이와 함께 새 연결 문자열 키워드인 `MarsConn`이 추가되었습니다. 이 키워드는 `true` 또는 `false` 값을 받으며, 기본값은 `false`입니다.  
  
 데이터 원본 속성 DBPROP_MULTIPLECONNECTIONS의 기본값은 VARIANT_TRUE입니다. 이것은 공급자가 다중 동시 명령 및 행 집합 개체를 지원하기 위해 다중 연결을 생성한다는 의미입니다. MARS가 설정 된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 있으므로 MULTIPLE_CONNECTIONS가 기본적으로 VARIANT_FALSE로 설정 되므로 Native Client는 단일 연결에서 여러 명령 및 행 집합 개체가 지원할 수 있습니다.  
  
 DBPROPSET_SQLSERVERDBINIT 속성 집합에 향상 된 기능에 대 한 자세한 내용은 참조 [초기화 및 권한 부여 속성](../../native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)합니다.  
  
### <a name="sql-server-native-client-ole-db-provider-example"></a>SQL Server Native Client OLE DB 공급자 예  
 이 예제에서는 데이터 원본 개체를 사용 하 여 만들어집니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 네이티브 OLE DB 공급자 및 MARS 설정 세션 개체를 만들기 전에 DBPROPSET_SQLSERVERDBINIT 속성을 사용 하 여 설정 되어 있습니다.  
  
```  
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
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 대 한 추가 MARS를 지원는 [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) 및 [SQLGetConnectAttr](../../native-client-odbc-api/sqlgetconnectattr.md) 함수입니다. SQL_MARS_ENABLED_YES 또는 SQL_MARS_ENABLED_NO를 받아들이는 SQL_COPT_SS_MARS_ENABLED가 추가되었으며 기본값은 SQL_MARS_ENABLED_NO입니다. 이와 함께 새 연결 문자열 키워드인 `Mars_Connection`이 추가되었습니다. 이 키워드는 "yes" 또는 "no" 값을 받으며, 기본값은 "no"입니다.  
  
### <a name="sql-server-native-client-odbc-driver-example"></a>SQL Server Native Client ODBC 드라이버 예  
 이 예제는 **SQLSetConnectAttr** 함수는 호출 하기 전에 MARS를 설정 하는 데 사용 되는 **SQLDriverConnect** 함수는 데이터베이스에 연결 합니다. 연결이 설정 되 면 두 개의 되 면 **SQLExecDirect** 함수는 동일한 연결에서 두 개의 별도 결과 집합을 만드는 데 호출 됩니다.  
  
```  
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
SQLExecDirect(hstmt1, L”SELECT * FROM Authors”, SQL_NTS);  
SQLExecDirect(hstmt2, L”SELECT * FROM Titles”, SQL_NTS);  
  
// Result set processing can interleave.  
SQLFetch(hstmt1);  
SQLFetch(hstmt2);  
```  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client 기능](sql-server-native-client-features.md)   
 [SQL Server 기본 결과 집합 사용](../../native-client-odbc-cursors/implementation/using-sql-server-default-result-sets.md)  
  
  
