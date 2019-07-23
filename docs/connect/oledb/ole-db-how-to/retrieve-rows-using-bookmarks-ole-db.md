---
title: 책갈피를 사용 하 여 행 검색 (OLE DB) | Microsoft Docs
description: 책갈피를 사용하여 행 검색(OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- bookmarks [OLE DB]
- rows [OLE DB]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: b2ab2e7be75e10ff97fcf254f885bfaa9dd25ec9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994711"
---
# <a name="retrieve-rows-using-bookmarks-ole-db"></a>책갈피를 사용하여 행 검색(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  소비자는 바인딩 구조의 **dwFlag** 필드 값을 DBCOLUMNSINFO_ISBOOKMARK로 설정하여 해당 열이 책갈피로 사용되도록 지정합니다. 소비자는 또한 행 집합 속성 DBPROP_BOOKMARKS를 VARIANT_TRUE로 설정합니다. 이렇게 하면 행 집합에 열 0이 포함될 수 있습니다. 그런 다음**IRowsetLocate::GetRowsAt** 을 사용하여 책갈피에서의 오프셋으로 지정된 행부터 시작하여 행을 인출합니다.  
  
> [!IMPORTANT]  
>  가능하면 Windows 인증을 사용하세요. Windows 인증을 사용할 수 없으면 런타임에 사용자에게 자격 증명을 입력하라는 메시지를 표시합니다. 자격 증명은 파일에 저장하지 않는 것이 좋습니다. 자격 증명을 유지하려면 [Win32 crypto API](https://go.microsoft.com/fwlink/?LinkId=64532)를 사용하여 자격 증명을 암호화해야 합니다.  
  
### <a name="to-retrieve-rows-using-bookmarks"></a>책갈피를 사용하여 행을 검색하려면  
  
1.  데이터 원본에 대한 연결을 설정합니다.  
  
2.  행 집합의 DBPROP_IRowsetLocate 속성을 VARIANT_TRUE로 설정합니다.  
  
3.  명령을 실행합니다.  
  
4.  책갈피로 사용할 열에 대해 바인딩 구조의 **dwFlag** 필드를 DBCOLUMNSINFO_ISBOOKMARK 플래그로 설정합니다.  
  
5.  **IRowsetLocate::GetRowsAt** 을 사용하여 책갈피에서의 오프셋으로 지정된 행부터 시작하여 행을 인출합니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 책갈피를 사용하여 행을 인출하는 방법을 보여 줍니다. 이 예제는 IA64에서 지원되지 않습니다.  
  
 이 예제에서 5번째 행은 SELECT 문을 실행하여 생성된 결과 집합에서 검색됩니다.  
  
 이 예제에는 [Microsoft SQL Server 예제 및 커뮤니티 프로젝트(Microsoft SQL Server Samples and Community Projects)](https://go.microsoft.com/fwlink/?LinkID=85384) 홈 페이지에서 다운로드할 수 있는 AdventureWorks 예제 데이터베이스가 필요합니다.  
  
 ole32.lib oleaut32.lib를 사용하여 컴파일하고 다음 C++ 코드 목록을 실행합니다. 이 애플리케이션은 컴퓨터의 기본 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결됩니다. 일부 Windows 운영 체제에서는 (localhost) 또는 (local)을 해당 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름으로 변경해야 합니다. 명명된 인스턴스에 연결하려면 연결 문자열을 L"(local)"에서 L"(local)\\\name"으로 변경합니다. 여기서 name은 명명된 인스턴스입니다. 기본적으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Express는 명명된 인스턴스에 설치됩니다. INCLUDE 환경 변수에 msoledbsql.h가 들어 있는 디렉터리를 포함해야 합니다.  
  
```  
// compile with: ole32.lib oleaut32.lib  
int InitializeAndEstablishConnection();  
int ProcessResultSet();  
  
#define UNICODE  
#define _UNICODE  
#define DBINITCONSTANTS  
#define INITGUID  
#define OLEDBVER 0x0250   // to include correct interfaces  
  
#include <stdio.h>  
#include <tchar.h>  
#include <stddef.h>  
#include <windows.h>  
#include <iostream>  
#include <oledb.h>  
#include <msoledbsql.h>  
  
using namespace std;  
  
IDBInitialize*       pIDBInitialize      = NULL;  
IDBProperties*       pIDBProperties      = NULL;  
IDBCreateSession*    pIDBCreateSession   = NULL;  
IDBCreateCommand*    pIDBCreateCommand   = NULL;  
ICommandProperties*  pICommandProperties = NULL;  
ICommandText*        pICommandText       = NULL;  
IRowset*             pIRowset            = NULL;  
IColumnsInfo*        pIColumnsInfo       = NULL;  
DBCOLUMNINFO*        pDBColumnInfo       = NULL;  
IAccessor*           pIAccessor          = NULL;  
IRowsetLocate*       pIRowsetLocate      = NULL;  
  
DBPROP        InitProperties[4];  
DBPROPSET     rgInitPropSet[1];   
DBPROPSET     rgPropSets[1];  
DBPROP        rgProperties[1];  
ULONG         i, j;                
HRESULT       hresult;  
DBROWCOUNT    cNumRows = 0;  
DBORDINAL     lNumCols;  
WCHAR*        pStringsBuffer;  
DBBINDING*    pBindings;  
DBLENGTH      ConsumerBufferColOffset = 0;  
HACCESSOR     hAccessor;  
DBCOUNTITEM   lNumRowsRetrieved;  
HROW          hRows[5];           
HROW*         pRows = &hRows[0];  
char*         pBuffer;  
  
int main() {  
   // The command to execute.  
   // WCHAR* wCmdString = OLESTR(" SELECT title_id, title FROM titles ");  
   WCHAR* wCmdString = OLESTR(" SELECT Name FROM Production.Product");  
  
   // Initialize and establish a connection to the data source.  
   if (InitializeAndEstablishConnection() == -1) {  
      // Handle error.  
      cout << "Failed to initialize and connect to the server.\n";  
      return -1;  
   }  
  
   // Create a session object.  
   if (FAILED(pIDBInitialize->QueryInterface(IID_IDBCreateSession, (void**) &pIDBCreateSession))) {  
      cout << "Failed to obtain IDBCreateSession interface.\n";  
      // Handle error.  
      return -1;  
   }  
  
   if (FAILED(pIDBCreateSession->CreateSession(NULL, IID_IDBCreateCommand, (IUnknown**) &pIDBCreateCommand))) {  
      cout << "pIDBCreateSession->CreateSession failed.\n";  
      // Handle error.  
      return -1;  
   }  
  
   // Access the ICommandText interface.  
   if (FAILED(pIDBCreateCommand->CreateCommand( NULL, IID_ICommandText, (IUnknown**) &pICommandText))) {  
      cout << "Failed to access ICommand interface.\n";  
      // Handle error.  
      return -1;  
   }  
  
   // Set DBPROP_IRowsetLocate  
   if (FAILED(pICommandText->QueryInterface( IID_ICommandProperties, (void **) &pICommandProperties ))) {  
      cout << "Failed to obtain ICommandProperties interface.\n";  
      // Handle error.  
      return -1;  
   }  
  
   // Set DBPROP_IRowsetLocate to VARIANT_TRUE to get the IRowsetLocate interface.  
   VariantInit(&rgProperties[0].vValue);  
  
   rgPropSets[0].guidPropertySet = DBPROPSET_ROWSET;  
   rgPropSets[0].cProperties = 1;  
   rgPropSets[0].rgProperties = rgProperties;  
  
   // Set properties in the property group (DBPROPSET_ROWSET)   
   rgPropSets[0].rgProperties[0].dwPropertyID  = DBPROP_IRowsetLocate;  
   rgPropSets[0].rgProperties[0].dwOptions     = DBPROPOPTIONS_REQUIRED;  
   rgPropSets[0].rgProperties[0].colid         = DB_NULLID;  
   rgPropSets[0].rgProperties[0].vValue.vt     = VT_BOOL;  
   rgPropSets[0].rgProperties[0].vValue.boolVal= VARIANT_TRUE;  
  
   // Set the rowset properties.  
   hresult = pICommandText->QueryInterface( IID_ICommandProperties,(void **)&pICommandProperties);  
   if (FAILED(hresult)) {  
      printf("Failed to get ICommandProperties to set rowset properties.\n");  
      // Release any references and return.  
      return -1;  
   }  
  
   hresult = pICommandProperties->SetProperties(1, rgPropSets);  
   if (FAILED(hresult)) {  
      printf("Execute failed to set rowset properties.\n");  
      // Release any references and return.  
      return -1;  
   }   
  
   pICommandProperties->Release();  
  
   // Specify the command text.  
   if (FAILED(pICommandText->SetCommandText(DBGUID_DBSQL, wCmdString))) {  
      cout << "Failed to set command text.\n";  
      // Handle error.  
      return -1;  
   }  
  
   // Execute the command.  
   if (FAILED(hresult =   
      pICommandText->Execute( NULL, IID_IRowset, NULL, &cNumRows, (IUnknown **) &pIRowset))) {  
      cout << "Failed to execute command.\n";  
      // Handle error.  
      return -1;  
   }  
  
   ProcessResultSet();   
  
   pIRowset->Release();  
  
   // Free up memory.  
   pICommandText->Release();  
   pIDBCreateCommand->Release();  
   pIDBCreateSession->Release();  
  
   pIDBInitialize->Uninitialize();  
   pIDBInitialize->Release();  
  
   // Release COM library.  
   CoUninitialize();  
  
   return -1;  
}  
  
int InitializeAndEstablishConnection() {      
   // Initialize the COM library.  
   CoInitialize(NULL);  
  
   // Obtain access to the OLE DB Driver for SQL Server.  
   CoCreateInstance( CLSID_MSOLEDBSQL, NULL, CLSCTX_INPROC_SERVER, IID_IDBInitialize, (void **) &pIDBInitialize);  
  
   // Initialize the property values that are the same for each property.  
   for ( i = 0 ; i < 4 ; i++ ) {  
      VariantInit(&InitProperties[i].vValue);  
      InitProperties[i].dwOptions = DBPROPOPTIONS_REQUIRED;  
      InitProperties[i].colid = DB_NULLID;  
   }  
  
   // Server name.  
   InitProperties[0].dwPropertyID = DBPROP_INIT_DATASOURCE;  
   InitProperties[0].vValue.vt = VT_BSTR;  
   InitProperties[0].vValue.bstrVal = SysAllocString(L"(local)");  
  
   // Database.  
   InitProperties[1].dwPropertyID = DBPROP_INIT_CATALOG;  
   InitProperties[1].vValue.vt = VT_BSTR;  
   InitProperties[1].vValue.bstrVal = SysAllocString(L"AdventureWorks");  
  
   InitProperties[2].dwPropertyID = DBPROP_AUTH_INTEGRATED;   
   InitProperties[2].vValue.vt = VT_BSTR;  
   InitProperties[2].vValue.bstrVal = SysAllocString(L"SSPI");  
  
   // Construct the PropertySet array.  
   rgInitPropSet[0].guidPropertySet = DBPROPSET_DBINIT;  
   rgInitPropSet[0].cProperties = 4;  
   rgInitPropSet[0].rgProperties = InitProperties;  
  
   // Set initialization properties.  
   pIDBInitialize->QueryInterface(IID_IDBProperties, (void **)&pIDBProperties);  
  
   hresult = pIDBProperties->SetProperties(1, rgInitPropSet);   
   if (FAILED(hresult)) {  
      cout << "Failed to set initialization properties.\n";  
      // Handle error.  
      return -1;  
   }  
  
   pIDBProperties->Release();  
  
   // Call the initialization method to establish the connection.  
   if (FAILED(pIDBInitialize->Initialize())) {  
      cout << "Problem initializing and connecting to the data source.\n";  
      // Handle error.  
      return -1;  
   }  
  
   return 0;  
}  
  
#ifdef _WIN64  
#define BUFFER_ALIGNMENT 8  
#else  
#define BUFFER_ALIGNMENT 4  
#endif  
  
#define ROUND_UP(value) (value + (BUFFER_ALIGNMENT - 1) & ~(BUFFER_ALIGNMENT - 1))  
  
int ProcessResultSet() {  
   HRESULT hr;  
  
   // Retrieve 5th row from the rowset (for example).  
   DBBKMARK iBookmark = 5;  
  
   pIRowset->QueryInterface(IID_IColumnsInfo, (void **)&pIColumnsInfo);  
  
   pIColumnsInfo->GetColumnInfo( &lNumCols, &pDBColumnInfo, &pStringsBuffer );  
  
   // Create a DBBINDING array.  
   pBindings = new DBBINDING[lNumCols];  
   if (!(pBindings /* = new DBBINDING[lNumCols] */ )) {  
      // Handle error.  
      return -1;  
   }  
  
   // Using the ColumnInfo strucuture, fill out the pBindings array.  
   for ( j = 0 ; j < lNumCols ; j++ ) {  
      pBindings[j].iOrdinal  = j;  
      pBindings[j].obValue   = ConsumerBufferColOffset;  
      pBindings[j].pTypeInfo = NULL;  
      pBindings[j].pObject   = NULL;  
      pBindings[j].pBindExt  = NULL;  
      pBindings[j].dwPart    = DBPART_VALUE;  
      pBindings[j].dwMemOwner = DBMEMOWNER_CLIENTOWNED;  
      pBindings[j].eParamIO  = DBPARAMIO_NOTPARAM;  
      pBindings[j].cbMaxLen  = pDBColumnInfo[j].ulColumnSize + 1;   // + 1 for null terminator  
      pBindings[j].dwFlags   = 0;  
      pBindings[j].wType      = pDBColumnInfo[j].wType;  
      pBindings[j].bPrecision = pDBColumnInfo[j].bPrecision;  
      pBindings[j].bScale     = pDBColumnInfo[j].bScale;  
  
      // Recalculate the next buffer offset.  
      ConsumerBufferColOffset = ConsumerBufferColOffset + pDBColumnInfo[j].ulColumnSize;  
  ConsumerBufferColOffset = ROUND_UP(ConsumerBufferColOffset);  
  
   };  
   // Indicate that the first field is used as a bookmark by setting  
   // dwFlags to DBCOLUMNFLAGS_ISBOOKMARK.  
   pBindings[0].dwFlags = DBCOLUMNFLAGS_ISBOOKMARK;  
  
   // Get IAccessor interface.  
   hr = pIRowset->QueryInterface( IID_IAccessor, (void **)&pIAccessor);  
   if (FAILED(hr)) {  
      printf("Failed to get IAccessor interface.\n");  
      // Handle error.  
      return -1;  
   }  
  
   // Create accessor.  
   hr = pIAccessor->CreateAccessor( DBACCESSOR_ROWDATA,  
                                    lNumCols,  
                                    pBindings,  
                                    0,  
                                    &hAccessor,  
                                    NULL);  
  
   if (FAILED(hr)) {  
      printf("Failed to create an accessor.\n");  
      // Handle error.  
      return -1;  
   }  
  
   hr = pIRowset->QueryInterface( IID_IRowsetLocate, (void **) &pIRowsetLocate);  
   if (FAILED(hr)) {  
      printf("Failed to get IRowsetLocate interface.\n");  
      // Handle error.  
      return -1;  
   }  
  
   hr = pIRowsetLocate->GetRowsAt( 0,  
                                   NULL,  
                                   sizeof(DBBKMARK),  
                                   (BYTE *) &iBookmark,  
                                   0,  
                                   1,  
                                   &lNumRowsRetrieved,  
                                   &pRows);  
  
   if (FAILED(hr)) {  
      printf("Calling the GetRowsAt method failed.\n");  
      // Handle error.  
      return -1;  
   }  
  
   // Create buffer and retrieve data.  
   pBuffer = new char[ConsumerBufferColOffset];  
   if (!(pBuffer /* = new char[ConsumerBufferColOffset] */ )) {  
      // Handle error.  
      return -1;  
   }  
  
   memset(pBuffer, 0, ConsumerBufferColOffset);  
  
   hr = pIRowset->GetData(hRows[0], hAccessor, pBuffer);  
   if (FAILED(hr)) {  
      printf("Failed GetDataCall.\n");  
      // Handle error.  
      return -1;  
   }  
  
   char szTitle[7] = {0};  
   strncpy_s(szTitle, &pBuffer[pBindings[1].obValue], 6);  
  
   printf("%S\n", &pBuffer[pBindings[1].obValue]);  
  
   pIRowset->ReleaseRows(lNumRowsRetrieved, hRows, NULL, NULL, NULL);  
  
   // Release allocated memory.  
   delete [] pBuffer;  
   pIAccessor->ReleaseAccessor(hAccessor, NULL);  
   pIAccessor->Release();  
   delete [] pBindings;  
  
   return 0;  
}  
```  
  
  
