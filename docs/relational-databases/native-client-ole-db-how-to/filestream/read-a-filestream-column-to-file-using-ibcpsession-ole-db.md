---
description: SQL Server Native Client (OLE DB)에서 IBCPSession를 사용 하 여 파일에 대 한 FILESTREAM 열 읽기
title: FILESTREAM to File, IBCPSession (OLE DB)
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: ab3ce02a-549d-4e01-87b9-d15281fba349
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5c48614682a028ef06279dea44631bd03acf055f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464904"
---
# <a name="read-a-filestream-column-to-file-using-ibcpsession-in-sql-server-native-client-ole-db"></a>SQL Server Native Client (OLE DB)에서 IBCPSession를 사용 하 여 파일에 대 한 FILESTREAM 열 읽기
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  이 예제에서는 IBCPSession 인터페이스를 사용하여 파일에 대한 filestream 열을 읽고 서식 파일을 씁니다.  
  
 Filestream 기능에 대 한 자세한 내용은 [Filestream Support &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/filestream-support-ole-db.md)를 참조 하세요.  
  
## <a name="example"></a>예제  
 INCLUDE 환경 변수에 sqlncli.h가 들어 있는 디렉터리를 포함해야 합니다.  
  
 다음 예제 중 하나를 사용하여 이 예제에서 읽어들이는 테이블을 만듭니다.  
  
-   [ICommandText 매개 변수에 바인딩된 ISequentialStream을 사용하여 FILESTREAM 열에 데이터 전송&#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-how-to/filestream/send-data-to-filestream-isequentialstream-bound-to-icommandtext.md)  
  
-   [IRowsetFastUpload를 사용하여 FILESTREAM 열에 데이터 전송&#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-how-to/filestream/send-data-to-a-filestream-column-using-irowsetfastupload-ole-db.md)  
  
 첫 번째 코드 목록을 복사하고 ISSHelper.h라는 파일로 붙여 넣습니다.  
  
 두 번째 코드 목록을 복사하고 ISSHelper.cpp라는 파일로 붙여 넣습니다.  
  
 세 번째 코드 목록을 복사하고 IBCPSession.cpp라는 파일로 붙여 넣습니다.  
  
 IBCPSession.cpp, ISSHelper.cpp, ole32.lib 및 oleaut32.lib를 컴파일합니다.  
  
 이 예제를 실행할 때는 서버 이름이나 server\instance_name 및 작성할 서식 파일 이름을 전달해야 합니다.  
  
```cpp
// ISSHelper.h: interface for the CISSHelper class.  
  
#if !defined(AFX_ISSHELPER_H__7B88E5F3_263F_11D2_9D1F_00C04F96B8B2__INCLUDED_)  
#define AFX_ISSHELPER_H__7B88E5F3_263F_11D2_9D1F_00C04F96B8B2__INCLUDED_  
  
#if _MSC_VER > 1000  
#pragma once  
#endif // _MSC_VER > 1000  
  
class CISSHelper : public ISequentialStream  {  
public:  
   // Constructor/destructor.  
   CISSHelper(__int64 i64LobBytes);  
   virtual ~CISSHelper();  
  
   // Helper function to clean up memory.  
   virtual void Clear();  
  
   // ISequentialStream interface implementation.  
   STDMETHODIMP_(ULONG)AddRef(void);  
   STDMETHODIMP_(ULONG)Release(void);  
   STDMETHODIMP QueryInterface(REFIID riid, LPVOID *ppv);  
   STDMETHODIMP Read(   
      /* [out] */ void __RPC_FAR *pv,  
      /* [in] */ ULONG cb,  
      /* [out] */ ULONG __RPC_FAR *pcbRead);  
   STDMETHODIMP Write(   
      /* [in] */ const void __RPC_FAR *pv,  
      /* [in] */ ULONG cb,  
      /* [out] */ ULONG __RPC_FAR *pcbWritten);  
  
public:  
   void * m_pBuffer;   // Buffer  
   ULONG m_ulLength;   // Total buffer size.  
   ULONG m_ulStatus;   // Column status.  
  
   __int64 m_i64BytesUploaded;  
   __int64 m_i64LastPrintUploaded;  
   __int64 m_i64ThreshHold;  
   DWORD m_dwStartTick;  
   DWORD m_dwParamOrdinal;  
  
private:  
   ULONG m_cRef;   // Reference count (not used).  
   ULONG m_iReadPos;   // Current index position for reading from the buffer.  
   ULONG m_iWritePos;   // Current index position for writing to the buffer.  
};  
  
#endif // !defined(AFX_ISSHELPER_H__7B88E5F3_263F_11D2_9D1F_00C04F96B8B2__INCLUDED_)  
```  
  
```cpp
// ISSHelper.cpp: implementation of the CISSHelper class.  
  
#pragma once  
#define WIN32_LEAN_AND_MEAN   // Exclude rarely-used stuff from Windows headers  
#include <stdio.h>  
#include <conio.h>  
#include <tchar.h>  
#include <sqlncli.h>  
#include "ISSHelper.h"  
  
#ifdef _DEBUG  
#undef THIS_FILE  
static char THIS_FILE[]=__FILE__;  
#define new DEBUm_NEW  
#endif  
  
// Implementation of ISequentialStream interface  
CISSHelper::CISSHelper(__int64 i64LobBytes) {  
   m_cRef= 0;  
   m_pBuffer= NULL;  
   m_ulLength= 0;  
   m_ulStatus   = DBSTATUS_S_OK;  
   m_iReadPos= 0;  
   m_iWritePos= 0;  
   m_i64ThreshHold = i64LobBytes;  
   m_i64BytesUploaded = 0;  
   m_i64LastPrintUploaded = 0;  
   m_dwStartTick = 0;  
   m_dwParamOrdinal = 0;  
}  
  
CISSHelper::~CISSHelper() {  
   Clear();  
}  
  
void CISSHelper::Clear() {  
   CoTaskMemFree( m_pBuffer );  
   m_cRef= 0;  
   m_pBuffer= NULL;  
   m_ulLength= 0;  
   m_ulStatus   = DBSTATUS_S_OK;  
   m_iReadPos= 0;  
   m_iWritePos= 0;  
}  
  
ULONG CISSHelper::AddRef() {  
   return ++m_cRef;  
}  
  
ULONG CISSHelper::Release() {  
   return --m_cRef;  
}  
  
HRESULT CISSHelper::QueryInterface( REFIID riid, void** ppv ) {  
   *ppv = NULL;  
   if ( riid == IID_IUnknown )   
      *ppv = this;  
   if ( riid == IID_ISequentialStream )   
      *ppv = this;  
   if ( *ppv ) {  
      ( (IUnknown*) *ppv )->AddRef();  
      return S_OK;  
   }  
   return E_NOINTERFACE;  
}  
  
HRESULT CISSHelper::Read( void *pv, ULONG cb, ULONG* pcbRead ) {  
   // Check parameters.  
   if ( pcbRead )   
      *pcbRead = 0;  
   if ( !pv )   
      return STG_E_INVALIDPOINTER;  
   if ( 0 == cb )   
      return S_OK;   
  
   // Cut out now if threshold is hit.  
   __int64 left = m_i64ThreshHold-m_i64BytesUploaded;  
   if (left < cb)  
      cb = (ULONG)left;  
  
   if (0 == m_dwStartTick)  
      m_dwStartTick = GetTickCount();  
  
   m_i64BytesUploaded += cb;  
  
   if (( m_i64BytesUploaded - m_i64LastPrintUploaded ) >= (1024*1024*4)) {  
      __int64 i64Elapsed = (__int64) GetTickCount()-m_dwStartTick;  
      __int64 i64BytesPerSecond = m_i64BytesUploaded*1000/i64Elapsed;  
      printf("Param=%lu TotalBytes=%010I64u ElapsedMS=%010I64u BytesPerSec=%010I64u\n",   
         m_dwParamOrdinal, m_i64BytesUploaded, i64Elapsed, i64BytesPerSecond );  
      m_i64LastPrintUploaded = m_i64BytesUploaded;  
   }  
  
   if ( cb == left ) {  
      __int64 i64Elapsed = (__int64) GetTickCount()-m_dwStartTick;  
      __int64 i64BytesPerSecond = ( ( (m_i64BytesUploaded * 1000) / i64Elapsed) > 0 )  ? i64Elapsed : 1;  
      // __int64 i64BytesPerSecond = m_i64BytesUploaded * 1000 / (i64Elapsed > 0 ) ? i64Elapsed : 1;  
      printf("Last read:\nParam=%lu TotalBytes=%010I64u ElapsedMS=%010I64u BytesPerSec=%010I64u\n",   
         m_dwParamOrdinal, m_i64BytesUploaded, i64Elapsed, i64BytesPerSecond );  
      m_i64LastPrintUploaded = m_i64BytesUploaded;  
   }  
  
   if (pcbRead)  
      *pcbRead = cb;  
  
   return S_OK;  
}  
  
HRESULT CISSHelper::Write( const void *pv, ULONG cb, ULONG* pcbWritten ) {  
   // Check parameters.  
   if ( !pv )   
      return STG_E_INVALIDPOINTER;  
   if ( pcbWritten )   
      *pcbWritten = 0;  
   if ( 0 == cb )   
      return S_OK;  
  
   // Enlarge the current buffer.  
   m_ulLength += cb;  
  
   // Grow internal buffer to new size.  
   m_pBuffer = CoTaskMemRealloc( m_pBuffer, m_ulLength );  
  
   // Check for out of memory situation.  
   if ( NULL == m_pBuffer ) {  
      Clear();  
      return E_OUTOFMEMORY;  
   }  
  
   // Copy callers memory to internal bufffer and update write position.  
   memcpy( (void*)((BYTE*)m_pBuffer + m_iWritePos), pv, cb );  
   m_iWritePos += cb;  
  
   // Return bytes written to caller.  
   if ( pcbWritten )   
      *pcbWritten = cb;  
  
   return S_OK;  
}  
```  
  
```cpp
//  IBCPSession.cpp  
#pragma once  
#define WIN32_LEAN_AND_MEAN// Exclude rarely-used stuff from Windows headers  
#include <stdio.h>  
#include <conio.h>  
#include <tchar.h>  
#include <sqlncli.h>  
  
#define SAFE_RELEASE(x)    { if (x) { x->Release(); x = NULL; } }  
#define SAFE_SYSFREE(bstr) { if (bstr) { ::SysFreeString(bstr); bstr = NULL; } }  
#define CHECK_HR(hr,jump)  { if ( FAILED(hr) ) goto jump; }  
#define CHECK_HR_ERR(hr,jump)  { if ( FAILED(hr) ) { DumpErrorRecords(); goto jump; } }  
  
// Helper function for DumpErrorRecords() to convert a clisd to string representation of clsid.  
LPWSTR CLSIDToString( CLSID* pclsid ) {  
   static WCHAR wszCLSID[1024];  
   if ( NULL == pclsid )  
      wcscpy_s(wszCLSID, 1024, L"(Null)");     
   else  
      ::StringFromGUID2( *pclsid, (OLECHAR*)wszCLSID, sizeof(wszCLSID) );  
   return wszCLSID;  
}  
  
// Helper function to dump out OLE DB errors to console window.  
HRESULT DumpErrorRecords() {  
   HRESULT hr = S_OK;  
   IErrorRecords* pIErrorRecords = NULL;  
   IErrorInfo* pIErrorInfo = NULL;  
   IErrorInfo* pIErrorInfoRecord = NULL;  
   BSTR bstrDescription = NULL;  
   BSTR bstrSource = NULL;  
   ULONG i;  
   ULONG cRecords = 0;  
   LCID lcid = 0;  
   ERRORINFO ErrorInfo;  
  
   // Get IErrorInfo pointer from OLE.  
   hr = ::GetErrorInfo( 0, &pIErrorInfo );  
   if ( FAILED(hr) ) {  
      printf( "No error records found.\n" );  
      goto DumpErrorRecordsExit;  
   }  
  
   // QI for IID_IErrorRecords.  
   hr = pIErrorInfo->QueryInterface( IID_IErrorRecords, (void**)&pIErrorRecords );  
   if ( FAILED(hr) ) {  
      printf( "pIErrorInfo->QueryInterface(IID_IErrorRecords) failed with hr=0x%08x.\n", hr );  
      goto DumpErrorRecordsExit;  
   }  
  
   // Get error record count.  
   hr = pIErrorRecords->GetRecordCount( &cRecords );  
   if ( FAILED(hr) ) {  
      printf( "pIErrorRecords->GetRecordCount() failed with hr=0x%08x.\n", hr );  
      goto DumpErrorRecordsExit;  
   }  
  
   // Get system LCID  
   lcid = GetSystemDefaultLCID();   
  
   // Loop through the error records.  
   for ( i = 0 ; i < cRecords ; i++ ) {  
      // Get pIErrorInfo from pIErrorRecords.  
      hr = pIErrorRecords->GetErrorInfo( i, lcid, &pIErrorInfoRecord );  
  
      if ( SUCCEEDED(hr) ) {  
         // Get error description and source.  
         hr = pIErrorInfoRecord->GetDescription( &bstrDescription );  
         hr = pIErrorInfoRecord->GetSource( &bstrSource );  
  
         // Retrieve the ErrorInfo structures.  
         hr = pIErrorRecords->GetBasicErrorInfo( i, &ErrorInfo );  
  
         // Dump out error.  
         printf( "\n" );  
         printf( "Dumping error record %lu of %lu:\n", i+1, cRecords );  
         printf( "--------------------------------------------------------------------------\n" );  
         printf( "   Description = %S\n", bstrDescription );  
         printf( "   Source      = %S\n", bstrSource );  
         printf( "   ERRORINFO.hrError = 0x%08x\n", ErrorInfo.hrError );  
         printf( "   ERRORINFO.dwMinor = %lu\n",ErrorInfo.dwMinor );   
         printf( "   ERRORINFO.clsid   = %S\n",CLSIDToString( &ErrorInfo.clsid ) );  
  
         SAFE_RELEASE(pIErrorInfoRecord);  
         SAFE_SYSFREE(bstrDescription);  
         SAFE_SYSFREE(bstrSource);  
      }  
   }  
  
DumpErrorRecordsExit:  
   SAFE_RELEASE(pIErrorInfoRecord);  
   SAFE_RELEASE(pIErrorRecords);  
   SAFE_RELEASE(pIErrorInfo);  
   SAFE_RELEASE(pIErrorInfo);  
   SAFE_SYSFREE(bstrDescription);  
   SAFE_SYSFREE(bstrSource);  
   return hr;  
}  
  
// to open a session  
  
// 1) create a properties object  
// 2) set properties on it (such as INIT_DATASOURCE, etc.)  
// 3) queryinterface an IDBInitialize on the properties object  
// 4) call IDBInitialize::Initialize  
// 5) queryinterface an IDBCreateSession on the IDBInitialize instance  
// 6) call IDBCreateSession::CreateSession with interface to use on the session (IDBCreateCommand, IOpenRowset, IBCPSession, etc.)  
  
HRESULT OpenSession( wchar_t* datasource, wchar_t* catalog, const IID& iid, void** out ) {  
#define SET_BSTR_PROP(index, proparray, propid, value) \  
   { proparray[index].dwOptions = DBPROPOPTIONS_REQUIRED; \  
   proparray[index].colid = DB_NULLID; \  
   proparray[index].dwStatus = DBPROPSTATUS_OK; \  
   proparray[index].dwPropertyID = propid; \  
   proparray[index].vValue.vt = VT_BSTR; \  
   proparray[index].vValue.bstrVal = SysAllocString(value); }  
  
#define SET_BOOL_PROP(index, proparray, propid, value) \  
   { proparray[index].dwOptions = DBPROPOPTIONS_REQUIRED; \  
   proparray[index].colid = DB_NULLID; \  
   proparray[index].dwStatus = DBPROPSTATUS_OK; \  
   proparray[index].dwPropertyID = propid; \  
   proparray[index].vValue.vt = VT_BOOL; \  
   proparray[index].vValue.boolVal = (value) ? VARIANT_TRUE : VARIANT_FALSE; }  
  
   HRESULT hr;  
  
   IDBProperties*     pIDBProperties = NULL;  
   IDBProperties*     pIDBSessionProperties = NULL;  
   IDBInitialize*     pIDBInitialize = NULL;    
   IDBCreateSession*  pIDBCreateSession = NULL;  
  
   DBPROP      InitProperties[3];  
   DBPROP      BulkCopyProperties[2];  
   DBPROPSET   PropSet[2];  
  
   hr = CoCreateInstance( SQLNCLI_CLSID, NULL, CLSCTX_INPROC_SERVER, IID_IDBProperties,   
      (void **) &pIDBProperties );      
   CHECK_HR(hr,OpenSessionCleanup);  
  
   // Hard coded this to point to local sql server, change as needed.  
   SET_BSTR_PROP( 0, InitProperties, DBPROP_INIT_DATASOURCE, datasource );  
   SET_BSTR_PROP( 1, InitProperties, DBPROP_INIT_CATALOG, catalog );  
   SET_BSTR_PROP( 2, InitProperties, DBPROP_AUTH_INTEGRATED, L"SSPI" );  
  
   SET_BOOL_PROP( 0, BulkCopyProperties, SSPROP_ENABLEFASTLOAD, true );  
   SET_BOOL_PROP( 1, BulkCopyProperties, SSPROP_ENABLEBULKCOPY, true );  
  
   PropSet[0].guidPropertySet = DBPROPSET_DBINIT;   
   PropSet[0].cProperties = 3;                 
   PropSet[0].rgProperties = InitProperties;   
  
   PropSet[1].guidPropertySet = DBPROPSET_SQLSERVERDATASOURCE;  
   PropSet[1].cProperties = 2;  
   PropSet[1].rgProperties = BulkCopyProperties;  
  
   pIDBProperties->SetProperties( 1, (DBPROPSET*) &PropSet );  
   CHECK_HR( hr, OpenSessionCleanup );  
  
   hr = pIDBProperties->QueryInterface( IID_IDBInitialize, (void**) &pIDBInitialize );  
   CHECK_HR( hr,OpenSessionCleanup );  
  
   hr = pIDBInitialize->Initialize();  
   CHECK_HR( hr,OpenSessionCleanup );  
  
   // QI for IID_IDBCreateSession and then create session.  
   hr = pIDBInitialize->QueryInterface( IID_IDBCreateSession, (void**) &pIDBCreateSession );  
   CHECK_HR( hr,OpenSessionCleanup );  
  
   pIDBCreateSession->QueryInterface( IID_IDBProperties, (void**) &pIDBSessionProperties );  
   pIDBSessionProperties->SetProperties( 1, &PropSet[1] );  
  
   hr = pIDBCreateSession->CreateSession( NULL, iid, (IUnknown**) out );  
  
OpenSessionCleanup:  
   SAFE_RELEASE( pIDBProperties );  
   SAFE_RELEASE( pIDBInitialize );  
   SAFE_RELEASE( pIDBCreateSession );  
   SAFE_RELEASE( pIDBSessionProperties );  
   return hr;      
}  
  
int wmain(int argc, wchar_t* argv[]) {  
   HRESULT hr;  
   IBCPSession * pIBCPSession = NULL;  
   DBROWCOUNT rows;  
  
   CoInitialize(NULL);  
  
   if ( argc < 2 ) {  
      printf( "Usage: IBCPSession <server> <file> [<error file>]\n");  
      return 0;  
   }  
  
   // Open connection to database.  
   hr = OpenSession( argv[1], L"master", IID_IBCPSession, (void**) &pIBCPSession );  
   CHECK_HR_ERR(hr,MainCleanup);  
  
   // change the last parameter to BCP_DIRECTION_IN to make it write a file into the server  
   hr = pIBCPSession->BCPInit( L"[DBFsa]..[FSTRTable]", argv[2], (argc > 3) ? argv[3] : NULL, BCP_DIRECTION_OUT );  
   CHECK_HR_ERR( hr, MainCleanup );  
  
#define WRITE_FMT_FILE 1  
#if WRITE_FMT_FILE  
  
   hr = pIBCPSession->BCPColumns( 3 );  
   CHECK_HR_ERR( hr, MainCleanup );  
  
   hr = pIBCPSession->BCPColFmt( 1, BCP_TYPE_DEFAULT, BCP_PREFIX_DEFAULT, BCP_LENGTH_VARIABLE, NULL, 0, 1 );  
   CHECK_HR_ERR( hr, MainCleanup );  
  
   hr = pIBCPSession->BCPColFmt( 2, BCP_TYPE_DEFAULT, BCP_PREFIX_DEFAULT, BCP_LENGTH_VARIABLE, NULL, 0, 2 );  
   CHECK_HR_ERR( hr, MainCleanup );  
  
   hr = pIBCPSession->BCPColFmt( 3, BCP_TYPE_DEFAULT, BCP_PREFIX_DEFAULT, BCP_LENGTH_VARIABLE, NULL, 0, 3 );  
   CHECK_HR_ERR( hr, MainCleanup );  
  
   hr = pIBCPSession->BCPWriteFmt( L"fstrtable.fmt" );  
   CHECK_HR_ERR( hr, MainCleanup );  
  
#else  
  
   hr = pIBCPSession->BCPReadFmt( L"fstrtable.fmt" );  
   CHECK_HR_ERR( hr, MainCleanup );  
  
#endif  
  
   hr = pIBCPSession->BCPExec( &rows );  
   CHECK_HR_ERR( hr, MainCleanup );  
  
   hr = pIBCPSession->BCPDone();  
   CHECK_HR_ERR( hr, MainCleanup );  
  
MainCleanup:  
   SAFE_RELEASE( pIBCPSession );  
  
   printf_s( "Test complete.\n" );  
}  
```  
  
  
