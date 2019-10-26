---
title: FAST_FORWARD 커서 가져오기 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fast forward-only cursors
ms.assetid: 931a28c3-8ea1-45d6-9ca1-2b8388c4d8b0
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ec168903543e42dff34d03086949bee79829f328
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909537"
---
# <a name="obtain-a-fast_forward-cursor"></a>FAST_FORWARD 커서 가져오기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  정방향 전용, 읽기 전용 커서를 가져오려면 행 집합 속성 DBPROP_SERVERCURSOR, DBPROP_OTHERINSERT, DBPROP_OTHERUPDATEDELETE, DBPROP_OWNINSERT 및 DBPROP_OWNUPDATEDELETE를 VARIANT_TRUE로 설정합니다.  
  
 전체 예제에서는 행 집합 속성을 설정하여 FAST_FORWARD 커서를 가져오는 방법을 보여 줍니다. 속성이 설정된 후에 SELECT 문이 실행되어 **AdventureWorks** 데이터베이스에 있는 **Purchasing.Vendor** 테이블의 **Name** 열이 검색되고 표시됩니다.  
  
> [!IMPORTANT]  
>  가능하면 Windows 인증을 사용하세요. Windows 인증을 사용할 수 없으면 런타임에 사용자에게 자격 증명을 입력하라는 메시지를 표시합니다. 자격 증명은 파일에 저장하지 않는 것이 좋습니다. 자격 증명을 유지하려면 [Win32 crypto API](https://go.microsoft.com/fwlink/?LinkId=64532)를 사용하여 자격 증명을 암호화해야 합니다.  
  
### <a name="to-obtain-fast_forward-cursor"></a>FAST_FORWARD 커서를 가져오려면  
  
1.  데이터 원본에 대한 연결을 설정합니다.  
  
2.  행 집합 속성 DBPROP_SERVERCURSOR, DBPROP_OTHERINSERT, DBPROP_OTHERUPDATEDELETE, DBPROP_OWNINSERT 및 DBPROP_OWNUPDATEDELETE를 VARIANT_TRUE로 설정합니다.  
  
3.  명령을 실행합니다.  

## <a name="example"></a>예제  
 다음 예제에서는 행 집합 속성을 설정하여 FAST_FORWARD 커서를 가져오는 방법을 보여 줍니다. 속성이 설정된 후에 SELECT 문이 실행되어 AdventureWorks 데이터베이스에 있는 Purchasing.Vendor 테이블의 Name 열이 검색되고 표시됩니다. 이 예제는 IA64에서 지원되지 않습니다.  
  
 이 예제에는 [Microsoft SQL Server 예제 및 커뮤니티 프로젝트(Microsoft SQL Server Samples and Community Projects)](https://go.microsoft.com/fwlink/?LinkID=85384) 홈 페이지에서 다운로드할 수 있는 AdventureWorks 예제 데이터베이스가 필요합니다.  
  
 ole32.lib oleaut32.lib를 사용하여 컴파일하고 다음 C++ 코드 목록을 실행합니다. 이 애플리케이션은 컴퓨터의 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결됩니다. 일부 Windows 운영 체제에서는 (localhost) 또는 (local)을 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름으로 변경해야 합니다. 명명된 인스턴스에 연결하려면 연결 문자열을 L"(local)"에서 L"(local)\\\name"으로 변경합니다. 여기서 name은 명명된 인스턴스입니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express는 명명된 인스턴스에 설치됩니다. INCLUDE 환경 변수에 sqlncli.h가 들어 있는 디렉터리를 포함해야 합니다.  
  
```  
// compile with: ole32.lib oleaut32.lib  
#define INITGUID  
#define DBINITCONSTANTS  
#define OLEDBVER 0x0250   // to include correct interfaces  
  
#include <windows.h>  
#include <stdio.h>  
#include <oledb.h>  
#include <sqlncli.h>  
#include <oledberr.h>  
  
IDBInitialize* pIDBInitialize = NULL;  
ICommandText* pICommandText = NULL;  
  
// Connect to the server and create a command object.  
int InitializeAndConnect();  
  
// Set the properties to get a FAST_FORWARD cursor.  
int SetRowsetProperties();  
  
// This function executes a command and displays the results.  
int ExecuteAndDisplay();  
  
// Release memory.  
void Cleanup();  
  
int main() {  
   if (InitializeAndConnect() == -1) {  
      // Handle error.  
      printf("Failed to initialize and connect to the server.\n");  
      return -1;  
   }  
  
   // Set the row properties to FAST_FORWARD cursor.  
   if (SetRowsetProperties() == -1) {  
      // Handle error.  
      printf("Failed to set the rowset properties.\n");  
      return -1;  
   }  
  
   // Execute a command and display the results.  
   if (ExecuteAndDisplay() == -1) {  
      // Handle error.  
      printf("Failed to execute a command and display the results.\n");  
      return -1;  
   }  
  
   Cleanup();  
}  
  
int InitializeAndConnect() {  
   HRESULT hr = S_OK;  
  
   IDBProperties* pIDBProperties = NULL;  
   IDBCreateSession* pIDBCreateSession = NULL;  
   IDBCreateCommand* pIDBCreateCommand = NULL;  
  
   DBPROPSET dbPropSet;  
   DBPROP dbProp[4];  
   int iRetVal = 0;  
  
   // Initialize OLE  
   if ( FAILED( hr = OleInitialize( NULL ) ) ) {  
      // Handle errors here.  
      return -1;  
   }  
  
   // Create an instance of Microsoft SQL Server Native Client OLE DB Provider.  
   if ( FAILED( hr =   
      CoCreateInstance(CLSID_SQLNCLI11, NULL, CLSCTX_INPROC_SERVER, IID_IDBProperties, (void **) &pIDBProperties ))) {  
      // Handle errors here.  
      return -1;  
   }  
  
   // Set up the connection properties.  
   dbProp[0].dwPropertyID = DBPROP_INIT_DATASOURCE;  
   dbProp[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
   dbProp[0].colid = DB_NULLID;  
   V_VT(&(dbProp[0].vValue)) = VT_BSTR;  
  
   V_BSTR(&(dbProp[0].vValue)) = SysAllocString( L"(local)" );  
  
   dbProp[1].dwPropertyID = DBPROP_AUTH_INTEGRATED;  
   dbProp[1].dwOptions = DBPROPOPTIONS_REQUIRED;  
   dbProp[1].colid = DB_NULLID;  
   V_VT(&(dbProp[1].vValue)) = VT_BSTR;  
   V_BSTR(&(dbProp[1].vValue)) = SysAllocString( L"SSPI" );  
  
   dbProp[2].dwPropertyID = DBPROP_NULLCOLLATION;  
   dbProp[2].dwOptions = DBPROPOPTIONS_REQUIRED;  
   dbProp[2].colid = DB_NULLID;  
   V_VT(&(dbProp[2].vValue)) = VT_BSTR;  
   V_BSTR(&(dbProp[2].vValue)) = SysAllocString( L"" );  
  
   dbProp[3].dwPropertyID = DBPROP_INIT_CATALOG;  
   dbProp[3].dwOptions = DBPROPOPTIONS_REQUIRED;  
   dbProp[3].colid = DB_NULLID;  
   V_VT(&(dbProp[3].vValue)) = VT_BSTR;  
   V_BSTR(&(dbProp[3].vValue)) = SysAllocString( L"AdventureWorks" );  
  
   dbPropSet.rgProperties = dbProp;  
   dbPropSet.cProperties = 4;  
   dbPropSet.guidPropertySet = DBPROPSET_DBINIT;  
  
   if ( FAILED( hr = pIDBProperties->SetProperties( 1, &dbPropSet ))) {  
      // Handle errors here.  
      iRetVal = -1;  
      goto CLEANUP;  
   }  
  
   SysFreeString( V_BSTR(&(dbProp[0].vValue)) );  
   SysFreeString( V_BSTR(&(dbProp[1].vValue)) );  
   SysFreeString( V_BSTR(&(dbProp[2].vValue)) );  
   SysFreeString( V_BSTR(&(dbProp[3].vValue)) );  
  
   // Get an IDBInitialize interface.  
   if ( FAILED( hr =   
      pIDBProperties->QueryInterface( IID_IDBInitialize, (void **) &pIDBInitialize ))) {  
      // Handle errors here.  
      iRetVal = -1;  
      goto CLEANUP;  
   }  
  
   // Call Initialize.  
   if ( FAILED( hr = pIDBInitialize->Initialize())) {  
      // Handle errors here.  
      iRetVal = -1;  
      goto CLEANUP;  
   }  
  
   // Get a IDBCreateSession interface.  
   if ( FAILED( hr =   
      pIDBInitialize->QueryInterface( IID_IDBCreateSession, (void **) &pIDBCreateSession ))) {  
      // Handle errors here.  
      iRetVal = -1;  
      goto CLEANUP;  
   }  
  
   // Create a session  
   if ( FAILED( hr =   
      pIDBCreateSession->CreateSession( NULL, IID_IDBCreateCommand, (IUnknown **) &pIDBCreateCommand))) {  
      // Handle errors here.  
      iRetVal = -1;  
      goto CLEANUP;  
   }  
  
   // Create a command.  
   if ( FAILED( hr =   
      pIDBCreateCommand->CreateCommand( NULL, IID_ICommandText, (IUnknown **) &pICommandText))) {  
      // Handle errors here.  
      iRetVal = -1;  
      goto CLEANUP;  
   }  
  
CLEANUP:  
   // Release all the objects not needed anymore.  
   pIDBProperties->Release();  
   if ( pIDBCreateSession )  
      pIDBCreateSession->Release();  
   if ( pIDBCreateCommand )  
      pIDBCreateCommand->Release();  
  
   return iRetVal;  
}  
  
int SetRowsetProperties() {  
   HRESULT hr = S_OK;  
   ICommandProperties* pICommandProperties = NULL;  
   DBPROPSET dbPropSet;  
   DBPROP dbProp[5];  
   int iRetVal = 0;  
  
   // Get an ICommandProperties object.  
   if ( FAILED( hr =   
      pICommandText->QueryInterface( IID_ICommandProperties, (void **) &pICommandProperties ))) {  
      // Handle errors here.  
      return -1;  
   }  
  
   // Set up the properties to get a FAST_FORWARD cursor.  
   dbProp[0].dwPropertyID       = DBPROP_SERVERCURSOR;  
   dbProp[0].dwOptions          = DBPROPOPTIONS_REQUIRED;  
   dbProp[0].colid              = DB_NULLID;  
   V_VT(&(dbProp[0].vValue))    = VT_BOOL;  
   V_BOOL(&(dbProp[0].vValue))  = VARIANT_TRUE;  
  
   dbProp[1].dwPropertyID       = DBPROP_OTHERINSERT;  
   dbProp[1].dwOptions          = DBPROPOPTIONS_REQUIRED;  
   dbProp[1].colid              = DB_NULLID;  
   V_VT(&(dbProp[1].vValue))    = VT_BOOL;  
   V_BOOL(&(dbProp[1].vValue))  = VARIANT_TRUE;  
  
   dbProp[2].dwPropertyID       = DBPROP_OTHERUPDATEDELETE;  
   dbProp[2].dwOptions          = DBPROPOPTIONS_REQUIRED;  
   dbProp[2].colid              = DB_NULLID;  
   V_VT(&(dbProp[2].vValue))    = VT_BOOL;  
   V_BOOL(&(dbProp[2].vValue))  = VARIANT_TRUE;  
  
   dbProp[3].dwPropertyID       = DBPROP_OWNINSERT;  
   dbProp[3].dwOptions          = DBPROPOPTIONS_REQUIRED;  
   dbProp[3].colid              = DB_NULLID;  
   V_VT(&(dbProp[3].vValue))    = VT_BOOL;  
   V_BOOL(&(dbProp[3].vValue))  = VARIANT_TRUE;  
  
   dbProp[4].dwPropertyID       = DBPROP_OWNUPDATEDELETE;  
   dbProp[4].dwOptions          = DBPROPOPTIONS_REQUIRED;  
   dbProp[4].colid              = DB_NULLID;  
   V_VT(&(dbProp[4].vValue))    = VT_BOOL;  
   V_BOOL(&(dbProp[4].vValue))  = VARIANT_TRUE;  
  
   dbPropSet.rgProperties       = dbProp;  
   dbPropSet.cProperties        = 5;  
   dbPropSet.guidPropertySet    = DBPROPSET_ROWSET;  
  
   if ( FAILED( hr = pICommandProperties->SetProperties( 1, &dbPropSet))) {  
      // Handle errors here.  
      iRetVal = -1;  
   }  
  
   // Release the ICommandProperties object.  
   pICommandProperties->Release();  
  
   return iRetVal;  
}  
  
int ExecuteAndDisplay() {  
   HRESULT hr = S_OK;  
   IRowset* pIRowset = NULL;  
   IAccessor* pIAccessor = NULL;  
  
   BYTE* pData = NULL;  
   DBCOUNTITEM cRowsObtained = 0;  
   ULONG cCount = 0;  
  
   HROW* pRows = new HROW[10];  
   HACCESSOR hAccessor = 0;  
   DBBINDING Bind[1];  
   int iRetVal = 0;  
  
   if (!pRows)  
      return -1;  
  
   // Set the command text.  
   if ( FAILED( hr = pICommandText->SetCommandText( DBGUID_SQL, L"select Name from Purchasing.Vendor")))  
      // Handle errors and free the memory here.  
      return -1;  
  
   // Execute the command.  
   if ( FAILED( hr = pICommandText->Execute( NULL, IID_IRowset, NULL, NULL, (IUnknown **) &pIRowset )))  
      // Handle errors and free the memory here.  
      return -1;  
  
    // Set up the binding structure for Name (nvarchar(50)).  
    Bind[0].dwPart      = DBPART_VALUE;  
    Bind[0].eParamIO    = DBPARAMIO_NOTPARAM;  
    Bind[0].iOrdinal    = 1;  
    Bind[0].pTypeInfo   = NULL;  
    Bind[0].pObject     = NULL;  
    Bind[0].pBindExt    = NULL;  
    Bind[0].dwFlags     = 0;  
    Bind[0].dwMemOwner  = DBMEMOWNER_CLIENTOWNED;  
    Bind[0].obLength    = 0;  
    Bind[0].obStatus    = 0;  
    Bind[0].obValue     = 0;  
    Bind[0].cbMaxLen    = 102;  
    Bind[0].wType       = DBTYPE_WSTR;  
    Bind[0].bPrecision  = 0;  
    Bind[0].bScale      = 0;  
  
   // Get an IAccessor interface.  
   if ( FAILED( hr = pIRowset->QueryInterface( IID_IAccessor, (void **) &pIAccessor))) {  
      // Handle errors and free the memory here.  
      iRetVal = -1;  
      goto CLEANUP;  
   }  
  
   // Create an accessor.  
   if ( FAILED( hr =   
      pIAccessor->CreateAccessor(  DBACCESSOR_ROWDATA, 1, Bind, 0, &hAccessor, NULL))) {  
      // Handle errors and free the memory here.  
      iRetVal = -1;  
      goto CLEANUP;  
   }  
  
   // Allocate memory for the data.  
   pData = new BYTE[102];  
   if (!(pData /* = new BYTE[102] */ )) {  
      // Handle errors and free the memory here.  
      iRetVal = -1;  
      goto CLEANUP;  
   }  
  
   // Loop through all of the rows.  
   for ( ; ; ) {  
      if (FAILED( hr = pIRowset->GetNextRows( NULL, 0, 10, &cRowsObtained, &pRows))) {  
         // Handle errors and free the memory here.  
         iRetVal = -1;  
         goto CLEANUP;  
      }  
  
      // Make sure some rows were obtained.  
      if (cRowsObtained == 0)  
         break;  
  
      // Get the data for the each of the rows.  
      for ( cCount = 0 ; cCount < cRowsObtained ; cCount++ ) {  
         // Get the row data needed.  
         if ( FAILED( hr = pIRowset->GetData( pRows[cCount], hAccessor, pData ))) {  
            // Handle errors and free the memory here.  
            iRetVal = -1;  
            goto CLEANUP;  
         }  
  
         // Display row data.  
         printf( "%S\n", pData);  
      }  
  
      // Release the rows.  
      if ( FAILED( hr = pIRowset->ReleaseRows(cRowsObtained, pRows, NULL, NULL, NULL ))) {  
         // Handle errors and free the memory here.  
         iRetVal = -1;  
         goto CLEANUP;  
      }  
   }  
  
CLEANUP:  
   // Release memory allocated for the data.  
   delete [] pRows;  
   delete [] pData;  
  
   // Release the HACCESSOR.  
   if (pIAccessor) {  
      pIAccessor->ReleaseAccessor( hAccessor, NULL );  
  
      // Release the IAccessor object.  
      pIAccessor->Release();  
   }  
  
   // Release the rowset.  
   pIRowset->Release();  
  
   return iRetVal;  
}  
  
void Cleanup() {  
   HRESULT hr = S_OK;  
  
   // Release the ICommandText object.  
   pICommandText->Release();  
  
   // Uninitialize the IDBInitialize object.  
   if ( FAILED( hr = pIDBInitialize->Uninitialize())) {  
      // Handle errors here.  
   }  
  
   // Release the IDBInitialize object.  
   pIDBInitialize->Release();  
  
   // Uninitialize OLE.  
   OleUninitialize();  
}  
```  
  
  
