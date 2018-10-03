---
title: 결과 집합 (OLE DB)에서 행을 인출 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rows [OLE DB]
ms.assetid: 8e9916a5-61e1-468e-8a5c-1ab8b5110737
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 846a4d4852aa2cf115ee743167940b19fc8b701f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47810831"
---
# <a name="fetch-rows-from-a-result-set-ole-db"></a>결과 집합에서 행 인출(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  이 예제에서는 결과 집합에서 행을 인출하는 방법을 보여 줍니다. 이 예제는 IA64에서 지원되지 않습니다.  
  
 이 예제에는 [Microsoft SQL Server 예제 및 커뮤니티 프로젝트(Microsoft SQL Server Samples and Community Projects)](http://go.microsoft.com/fwlink/?LinkID=85384) 홈 페이지에서 다운로드할 수 있는 AdventureWorks 예제 데이터베이스가 필요합니다.  
  
> [!IMPORTANT]  
>  가능하면 Windows 인증을 사용하세요. Windows 인증을 사용할 수 없으면 런타임에 사용자에게 자격 증명을 입력하라는 메시지를 표시합니다. 자격 증명은 파일에 저장하지 않는 것이 좋습니다. 자격 증명을 유지하려면 [Win32 crypto API](http://go.microsoft.com/fwlink/?LinkId=64532)를 사용하여 자격 증명을 암호화해야 합니다.  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>Description  
 ole32.lib oleaut32.lib를 사용하여 컴파일하고 다음 C++ 코드 목록을 실행합니다. 이 응용 프로그램은 컴퓨터의 기본 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결됩니다. 일부 Windows 운영 체제에서는 (localhost) 또는 (local)을 해당 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름으로 변경해야 합니다. 명명된 인스턴스에 연결하려면 연결 문자열을 L"(local)"에서 L"(local)\\\name"으로 변경합니다. 여기서 name은 명명된 인스턴스입니다. 기본적으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Express는 명명된 인스턴스에 설치됩니다. INCLUDE 환경 변수에 sqlncli.h가 들어 있는 디렉터리를 포함해야 합니다.  
  
### <a name="code"></a>코드  
  
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
#include <sqlncli.h>  
#include <msdadc.h>   // for IDataConvert  
#include <msdaguid.h>   // for IDataConvert  
  
using namespace std;  
  
IDBInitialize* pIDBInitialize = NULL;  
IDBProperties* pIDBProperties = NULL;  
IDBCreateSession* pIDBCreateSession = NULL;  
IDBCreateCommand* pIDBCreateCommand = NULL;  
ICommandText* pICommandText = NULL;  
IRowset* pIRowset = NULL;  
IColumnsInfo* pIColumnsInfo = NULL;  
  
DBCOLUMNINFO* pDBColumnInfo = NULL;  
IAccessor* pIAccessor =  NULL;  
DBPROP InitProperties[4];  
DBPROPSET rgInitPropSet[1];  
  
ULONG i, j;  
HRESULT hr;  
DBROWCOUNT cNumRows = 0;  
DBORDINAL lNumCols;  
WCHAR* pStringsBuffer;  
DBBINDING* pBindings;  
DBLENGTH ConsumerBufColOffset = 0;  
HACCESSOR hAccessor;  
DBCOUNTITEM lNumRowsRetrieved;  
HROW hRows[10];  
HROW* pRows = &hRows[0];  
  
int main() {  
   // The command to execute.  
   WCHAR* wCmdString = OLESTR("SELECT StandardCost, ListPrice FROM Production.Product WHERE ListPrice > 14.00");  
  
   // Call a function to initialize and establish connection.   
   if (InitializeAndEstablishConnection() == -1) {  
      // Handle error.  
      cout << "Failed to initialize and connect to the server.\n";  
      return -1;  
   }  
  
   // Create a session object.  
   if (FAILED(pIDBInitialize->QueryInterface( IID_IDBCreateSession,  
      (void**) &pIDBCreateSession))) {  
         cout << "Failed to obtain IDBCreateSession interface.\n";  
         // Handle error.  
         return -1;  
   }  
  
   if (FAILED(pIDBCreateSession->CreateSession( NULL,   
      IID_IDBCreateCommand,   
      (IUnknown**) &pIDBCreateCommand))) {  
         cout << "pIDBCreateSession->CreateSession failed.\n";  
         // Handle error.  
         return -1;  
   }  
  
   // Access the ICommandText interface.  
   if (FAILED(pIDBCreateCommand->CreateCommand( NULL,   
      IID_ICommandText,   
      (IUnknown**) &pICommandText))) {  
         cout << "Failed to access ICommand interface.\n";  
         // Handle error.  
         return -1;  
   }  
  
   // Use SetCommandText() to specify the command text.  
   if (FAILED(pICommandText->SetCommandText(DBGUID_DBSQL, wCmdString))) {  
      cout << "Failed to set command text.\n";  
      // Handle error.  
      return -1;  
   }  
  
   // Execute the command.  
   if (FAILED(hr = pICommandText->Execute( NULL,   
      IID_IRowset,   
      NULL,   
      &cNumRows,   
      (IUnknown **) &pIRowset))) {  
         cout << "Failed to execute command.\n";  
         // Handle error.  
         return -1;  
   }  
  
   // Process the result set.  
   ProcessResultSet();   
  
   pIRowset->Release();  
  
   // Free up memory.  
   pICommandText->Release();  
   pIDBCreateCommand->Release();  
   pIDBCreateSession->Release();  
  
   if (FAILED(pIDBInitialize->Uninitialize())) {  
      // Uninitialize is not required, but it fails if an interface  
      // has not been released.  This can be used for debugging.  
      cout << "Problem uninitializing.\n";  
   }  
  
   pIDBInitialize->Release();  
   CoUninitialize();  
};  
  
int InitializeAndEstablishConnection() {      
   CoInitialize(NULL);  
  
   // Obtain access to the SQLNCLI provider.  
   hr = CoCreateInstance( CLSID_SQLNCLI11,  
      NULL,  
      CLSCTX_INPROC_SERVER,  
      IID_IDBInitialize,  
      (void **) &pIDBInitialize);  
  
   if (FAILED(hr)) {  
      printf("Failed to get IDBInitialize interface.\n");  
      // Handle errors here.  
      return -1;  
   }  
  
   // Initialize the property values needed to establish the connection.  
   for ( i = 0 ; i < 4 ; i++ )  
      VariantInit(&InitProperties[i].vValue);  
  
   // Server name.  
   InitProperties[0].dwPropertyID = DBPROP_INIT_DATASOURCE;  
   InitProperties[0].vValue.vt = VT_BSTR;  
  
   InitProperties[0].vValue.bstrVal= SysAllocString(L"(local)");  
   InitProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
   InitProperties[0].colid = DB_NULLID;  
  
   // Database.  
   InitProperties[1].dwPropertyID = DBPROP_INIT_CATALOG;  
   InitProperties[1].vValue.vt = VT_BSTR;  
   InitProperties[1].vValue.bstrVal = SysAllocString(L"AdventureWorks");  
   InitProperties[1].dwOptions = DBPROPOPTIONS_REQUIRED;  
   InitProperties[1].colid = DB_NULLID;  
  
   InitProperties[2].dwPropertyID = DBPROP_AUTH_INTEGRATED;  
   InitProperties[2].vValue.vt = VT_BSTR;  
   InitProperties[2].vValue.bstrVal = SysAllocString(L"SSPI");  
   InitProperties[2].dwOptions = DBPROPOPTIONS_REQUIRED;  
   InitProperties[2].colid = DB_NULLID;  
  
   // Properties are set, now construct the DBPROPSET structure (rgInitPropSet) used to pass   
   // an array of DBPROP structures (InitProperties) to the SetProperties method.  
   rgInitPropSet[0].guidPropertySet = DBPROPSET_DBINIT;  
   rgInitPropSet[0].cProperties = 4;  
   rgInitPropSet[0].rgProperties = InitProperties;  
  
   // Set initialization properties.  
   hr = pIDBInitialize->QueryInterface(IID_IDBProperties, (void **)&pIDBProperties);  
   if (FAILED(hr)) {  
      cout << "Failed to get IDBProperties interface.\n";  
      // Handle errors here.  
      return -1;  
   }  
  
   hr = pIDBProperties->SetProperties(1, rgInitPropSet);   
   if (FAILED(hr)) {  
      cout << "Failed to set initialization properties.\n";  
      // Handle errors here.  
      return -1;  
   }  
  
   pIDBProperties->Release();  
  
   // Now establish the connection to the data source.  
   if (FAILED(pIDBInitialize->Initialize())) {  
      cout << "Problem in establishing connection to the data"  
         "source.\n";  
      // Handle errors here.  
      return -1;  
   }  
   return 0;  
}  
  
// Retrieve and display data resulting from a query.  
int ProcessResultSet() {  
   // Obtain access to the IColumnInfo interface, from the Rowset object.  
   hr = pIRowset->QueryInterface(IID_IColumnsInfo, (void **)&pIColumnsInfo);  
   if (FAILED(hr)) {  
      cout << "Failed to get IColumnsInfo interface.\n";  
      // Handle errors here.  
      return -1;  
   }   
  
   // Retrieve the column information.  
   pIColumnsInfo->GetColumnInfo(&lNumCols, &pDBColumnInfo, &pStringsBuffer);  
  
   // Free the column information interface.  
   pIColumnsInfo->Release();  
  
   // Create a DBBINDING array.  
   DBBINDING * p = (pBindings = new DBBINDING[lNumCols]);  
   if (!(p /* pBindings = new DBBINDING[lNumCols] */ ))  
      return -1;  
  
   // Using the ColumnInfo structure, fill out the pBindings array.  
   for ( j = 0 ; j < lNumCols ; j++ ) {  
      pBindings[j].iOrdinal = j+1;  
      pBindings[j].obValue = ConsumerBufColOffset;  
      pBindings[j].pTypeInfo = NULL;  
      pBindings[j].pObject = NULL;  
      pBindings[j].pBindExt = NULL;  
      pBindings[j].dwPart = DBPART_VALUE;  
      pBindings[j].dwMemOwner = DBMEMOWNER_CLIENTOWNED;  
      pBindings[j].eParamIO = DBPARAMIO_NOTPARAM;  
      pBindings[j].cbMaxLen = (pDBColumnInfo[j].wType == DBTYPE_WSTR) ? pDBColumnInfo[j].ulColumnSize * 2 : pDBColumnInfo[j].ulColumnSize;  
      pBindings[j].dwFlags = 0;  
      pBindings[j].wType = pDBColumnInfo[j].wType;  
      pBindings[j].bPrecision = pDBColumnInfo[j].bPrecision;  
      pBindings[j].bScale = pDBColumnInfo[j].bScale;  
  
      // Compute the next buffer offset.  
      ConsumerBufColOffset =   
         ConsumerBufColOffset + pBindings[j].cbMaxLen;  
   };  
  
   // Get the IAccessor interface.  
   hr = pIRowset->QueryInterface(IID_IAccessor, (void **) &pIAccessor);  
   if (FAILED(hr)) {  
      cout << "Failed to obtain IAccessor interface.\n";  
      // Handle errors here.  
      return -1;  
   }  
  
   // Create an accessor from the set of bindings (pBindings).  
   pIAccessor->CreateAccessor(DBACCESSOR_ROWDATA, lNumCols, pBindings, 0, &hAccessor, NULL);  
  
   // Print column names.  
   for ( j = 0 ; j < lNumCols ; j++ )  
      printf("%-40S", pDBColumnInfo[j].pwszName);  
  
   printf("\n");   // new line after the column names  
  
   // Get a set of 10 rows.  
   pIRowset->GetNextRows( NULL, 0, 10, &lNumRowsRetrieved, &pRows);  
  
   // Allocate space for the row buffer.  
   BYTE * pBuffer = new BYTE[ConsumerBufColOffset];  
   if (!(pBuffer /* = new BYTE[ConsumerBufColOffset] */ )) {  
      // Free up all allocated memory.  
      pIAccessor->ReleaseAccessor(hAccessor, NULL);  
      pIAccessor->Release();  
      delete [] pBindings;  
  
      return 0;  
   }  
  
   // Create an instance of the data conversion library to convert DBTYPE_CY to string for display  
   IDataConvert* pIDataConvert;  
   CoCreateInstance(CLSID_OLEDB_CONVERSIONLIBRARY,  
      NULL,  
      CLSCTX_INPROC_SERVER,  
      IID_IDataConvert,  
      (void**)&pIDataConvert);  
  
   // variables used in DataConvert  
   DBLENGTH cbDstLength;  
   DBSTATUS dbsStatus;  
   char strCurrency0[25];  
   char strCurrency1[25];  
  
   // Display the rows.  
   while ( lNumRowsRetrieved > 0 ) {  
      // For each row, print the column data.  
      for ( j = 0 ; j < lNumRowsRetrieved ; j++ ) {  
         // Clear the buffer.  
         memset(pBuffer, 0, ConsumerBufColOffset);  
  
         // Get the row data values.  
         pIRowset->GetData(hRows[j], hAccessor, pBuffer);  
  
         // Convert DBTYPE_CY values to string   
         pIDataConvert->DataConvert(DBTYPE_CY,   // wSrcType  
            DBTYPE_STR,   // wDstType  
            sizeof(LARGE_INTEGER),   // cbSrcLength   
            &cbDstLength,   // pcbDstLength  
            &pBuffer[pBindings[0].obValue],   // pSrc  
            strCurrency0,   // pDst  
            sizeof(strCurrency0),   //cbDstMaxLength  
            DBSTATUS_S_OK,   // dbsSrcStatus  
            &dbsStatus,   // pdbsStatus  
            0,   // bPrecision (used for DBTYPE_NUMERIC only)  
            0,   // bScale (used for DBTYPE_NUMERIC only)  
            DBDATACONVERT_DEFAULT);   // dwFlags  
  
         pIDataConvert->DataConvert(DBTYPE_CY,   // wSrcType  
            DBTYPE_STR,   // wDstType  
            sizeof(LARGE_INTEGER),   // cbSrcLength   
            &cbDstLength,   // pcbDstLength  
            &pBuffer[pBindings[1].obValue],   // pSrc  
            strCurrency1,   // pDst  
            sizeof(strCurrency1),   // cbDstMaxLength  
            DBSTATUS_S_OK,   // dbsSrcStatus  
            &dbsStatus,   // pdbsStatus  
            0,   // bPrecision (used for DBTYPE_NUMERIC only)  
            0,   // bScale (used for DBTYPE_NUMERIC only)  
            DBDATACONVERT_DEFAULT); // dwFlags  
  
         // Print cost and price values.  
         printf("%-40s%s\n", strCurrency0, strCurrency1); //sparra  
      };  
  
      // Release the rows retrieved.  
      pIRowset->ReleaseRows(lNumRowsRetrieved, hRows, NULL, NULL, NULL);  
  
      // Get the next set of 10 rows.  
      pIRowset->GetNextRows(NULL, 0, 10, &lNumRowsRetrieved, &pRows);  
   }  
  
   // Free up all allocated memory.  
   delete [] pBuffer;  
   pIAccessor->ReleaseAccessor(hAccessor, NULL);  
   pIAccessor->Release();  
   delete [] pBindings;  
  
   return 0;  
}  
```  
  
## <a name="see-also"></a>관련 항목  
 [결과 처리 방법 도움말 항목&#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-how-to/results/processing-results-how-to-topics-ole-db.md)  
  
  
