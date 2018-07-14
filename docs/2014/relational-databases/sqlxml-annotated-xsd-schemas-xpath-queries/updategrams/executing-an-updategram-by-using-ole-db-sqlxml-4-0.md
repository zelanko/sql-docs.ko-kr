---
title: OLE DB (SQLXML 4.0)를 사용 하 여 Updategram 실행 | Microsoft Docs
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
- ICommandStream interface
- updategrams [SQLXML], OLE DB
- OLE DB, SQLXML
- executing updategrams [SQLXML]
ms.assetid: 4154c590-1541-49d0-8117-4ddf2ce5ccba
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7affd08d1b670fa653facb47f5aae5d0bd1d1aed
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37177737"
---
# <a name="executing-an-updategram-by-using-ole-db-sqlxml-40"></a>OLE DB를 사용하여 Updategram 실행(SQLXML 4.0)
  이 항목에서는 updategram을 실행 하는 DB usingOLE의 작업 예제를 제공 합니다.  
  
## <a name="using-icommandstream-to-set-an-xml-command"></a>ICommandStream을 사용하여 XML 명령 설정  
 OLE DB (버전 2.6 이상) ICommandStream 인터페이스를 문자열 대신 스트림 개체로 명령을 전달합니다.  
  
 이 인터페이스를 사용하면 XML 파서가 이해하는 모든 인코딩을 명령에 사용할 수 있습니다. Icommand:: Execute를 호출 하는 경우 명령 텍스트를 읽어 오며 스트림에 직접 및 변환이 필요 하지 않습니다. 인터페이스는 ICommandStream을 사용 하 여 XML 명령을 실행 합니다. 따라서 더 효율적입니다.  
  
### <a name="setting-xml-as-a-command-using-icommandstream-and-retrieving-the-results-as-an-xml-document"></a>ICommandStream을 사용하여 XML을 명령으로 설정 및 결과를 XML 문서로 검색  
 ICommandStream 인터페이스 수를 명령으로 XML 문서를 설정 하 고 결과 XML 문서로 검색할 수 있습니다.  
  
#### <a name="executing-templates-with-xpath-queries"></a>XPath 쿼리를 사용하여 템플릿 실행  
 XPath 쿼리로 구성 된 다음 XML 템플릿은 ICommandStream을 사용 하 여 명령으로 지정 됩니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<sql:xpath-query mapping-schema="Schema.xml">Person.Contact</sql:xpath-query>  
</ROOT>  
```  
  
 템플릿에 포함된 XPath 쿼리는 다음과 같은 매핑 스키마에 대해 실행됩니다.  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data" xmlns:dt="urn:schemas-microsoft-com:datatypes" xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<ElementType name="Person.Contact" >  
<AttributeType name="ContactID" />  
<AttributeType name="FirstName" />  
<AttributeType name="LastName" />  
<attribute type="ContactID" />  
<attribute type="FirstName" />  
<attribute type="LastName" />  
</ElementType>  
</Schema>  
```  
  
 쿼리에서 모든 직원 요소를 반환합니다. 기본 매핑을 사용 합니다  **\<Person.Contact >** 요소는 AdventureWorks 데이터베이스의 Person.Contact 테이블에 매핑됩니다.  
  
###### <a name="to-set-xml-as-a-command-and-retrieving-result-as-an-xml-document"></a>XML을 명령으로 설정하고 결과를 XML 문서로 검색하려면  
  
1.  데이터베이스에 대한 연결을 초기화하고 설정합니다.  
  
2.  ICommand의 ICommandStream 인터페이스를 가져옵니다.  
  
3.  필요한 명령 속성을 설정합니다. 이 예에서 공급자별 속성 SSPROP_STREAM_BASEPATH는 매핑 스키마와 템플릿 파일이 저장되는 디렉터리로 설정됩니다.  
  
4.  ICommandStream::SetCommandStream를 사용 하 여 명령 스트림을 지정 합니다. 이 예에서 실행되는 XML 템플릿은 파일에서 읽어옵니다. 이 기능은 큰 XML 템플릿을 실행하려는 경우에 유용합니다.  
  
5.  Icommand:: Execute를 IID_ISequentialStream 인터페이스 id입니다. 요청을 사용 하 여 XML 명령을 실행 합니다.  
  
6.  결과를 처리합니다. 이 예에서는 스트림에서 읽은 XML이 화면에 표시됩니다.  
  
    ```  
    void InitializeAndEstablishConnection();  
    void SetCommandProperties();  
    void ProcessResultSet();  
  
    #define UNICODE  
    #define _UNICODE  
    #define DBINITCONSTANTS  
    #define INITGUID  
  
    #include <stdio.h>  
    #include <tchar.h>  
    #include <stddef.h>  
    #include <windows.h>  
    #include <iostream.h>  
    #include <oledb.h>  
    #include <SQLOLEDB.h>  
  
    class CSequentialStream : public ISequentialStream  
    {  
       private:     
          ULONG       m_cRef;              // reference count  
          HANDLE      m_hFile;         // handle to the file  
          LPWSTR      m_wszFileName;      // the file name  
  
       public:  
          CSequentialStream( LPWSTR );  
          virtual ~CSequentialStream();  
  
          // IUnknown Methods  
          STDMETHODIMP_(ULONG)    AddRef();  
          STDMETHODIMP_(ULONG)    Release();  
          STDMETHODIMP QueryInterface( REFIID, LPVOID* );  
  
          // ISequentialStream Methods  
          STDMETHODIMP Read(   
                /* [out] */ void __RPC_FAR*,  
                /* [in]  */ ULONG,  
                /* [out] */ ULONG __RPC_FAR* );  
  
          STDMETHODIMP Write(   
                /* [in] */ const void __RPC_FAR*,  
                /* [in] */ ULONG,  
                /* [out]*/ ULONG __RPC_FAR* );  
    };  
  
    IDBInitialize*       pIDBInitialize     = NULL;  
    IDBProperties*       pIDBProperties     = NULL;  
    IDBCreateSession*    pIDBCreateSession  = NULL;  
    IDBCreateCommand*    pIDBCreateCommand  = NULL;  
    ICommand*            pICommand          = NULL;  
    ICommandStream*      pICommandStream    = NULL;  
    ICommandProperties*    pICommandProperties = NULL;  
    IColumnsInfo*        pIColumnsInfo      = NULL;  
    ISequentialStream*    pIXMLOutput      = NULL;  
    DBCOLUMNINFO*        pDBColumnInfo      = NULL;  
    IAccessor*           pIAccessor        =  NULL;  
    DBPROP               InitProperties[4];  
    DBPROPSET            rgInitPropSet[1];  
    ULONG                i, j;  
    HRESULT              hr;  
    LONG                 cNumRows = 0;  
    ULONG                lNumCols;  
    WCHAR*               pStringsBuffer;  
    DBBINDING*           pBindings;  
    ULONG                ConsumerBufColOffset = 0;  
    HACCESSOR            hAccessor;  
    ULONG                lNumRowsRetrieved;  
    HROW                 hRows[10];  
    HROW*                pRows = &hRows[0];  
    BYTE*                pBuffer;  
    CSequentialStream    XMLInput( L"Query.xml" );  
  
    CSequentialStream::CSequentialStream  
    (  
       LPWSTR      wszFileName  
    )  
    :  
       m_cRef( 0 ),  
       m_hFile( NULL ),  
       m_wszFileName( NULL )  
    {  
        // The constructor AddRefs.  
        AddRef();  
  
       // Allocate memory for the file name.  
       m_wszFileName = (LPWSTR) CoTaskMemAlloc( ( wcslen( wszFileName ) + 1 ) * 2 );  
  
       // Copy the file name.  
       wcscpy( m_wszFileName, wszFileName );  
    }  
  
    CSequentialStream::~CSequentialStream  
    (  
    )  
    {  
       // Free any allocated memory.  
       if( m_wszFileName )  
          CoTaskMemFree( m_wszFileName );  
  
       // Close the file.  
       if( m_hFile )  
          CloseHandle( m_hFile );  
    }  
  
    ULONG      
    CSequentialStream::AddRef  
    (  
    )  
    {  
        return ++m_cRef;  
    }  
  
    ULONG  
    CSequentialStream::Release()  
    {  
        if(--m_cRef)  
            return m_cRef;  
  
        delete this;  
        return 0;  
    }  
  
    HRESULT   
    CSequentialStream::QueryInterface  
    (     
       REFIID riid,   
       void** ppv  
    )  
    {  
        *ppv = NULL;  
  
        if (riid == IID_IUnknown)  
            *ppv = this;  
  
        if (riid == IID_ISequentialStream)  
            *ppv = this;  
  
        if(*ppv)  
        {  
            ((IUnknown*)*ppv)->AddRef();  
            return S_OK;  
        }  
  
        return E_NOINTERFACE;  
    }  
  
    HRESULT   
    CSequentialStream::Read  
    (  
       void *pv,   
       ULONG cb,   
       ULONG* pcbRead  
    )  
    {  
       ULONG   cBytesRead = 0;  
  
        // Parameter checking.  
        if(pcbRead)  
            *pcbRead = 0;  
  
        if(!pv)  
            return STG_E_INVALIDPOINTER;  
  
        if(cb == 0)  
            return S_OK;  
  
       // Do we need to open the file?  
       if( m_hFile == NULL )  
       {  
          // Open the file.  
          m_hFile = CreateFile( m_wszFileName, GENERIC_READ, 0, NULL, OPEN_EXISTING, 0, NULL );  
  
          // If the file failed to open, return E_FAIL.  
          if( m_hFile == INVALID_HANDLE_VALUE )  
             return E_FAIL;  
       }  
  
       // Clear the buffer.  
       ZeroMemory( pv, cb );  
  
       // Read cb bytes from the stream.  
       if( !ReadFile( m_hFile, pv, cb, &cBytesRead, NULL ) )  
          return E_FAIL;  
  
       // Inform the user of how many bytes to read.  
       if( NULL != pcbRead )   
          *pcbRead = cBytesRead;  
  
        if(cb != cBytesRead)  
            return S_FALSE;   
  
        return S_OK;  
    }  
  
    HRESULT   
    CSequentialStream::Write  
    (  
       const void *pv,   
       ULONG cb,   
       ULONG* pcbWritten  
    )  
    {  
       // For this example, only a read-only stream is needed.  
       return STG_E_CANTSAVE;  
    }  
  
    void main()   
    {  
       // Call a function to initialize and establish a connection.   
        InitializeAndEstablishConnection();  
  
        // Create a session object.  
        if(FAILED(pIDBInitialize->QueryInterface(  
                                    IID_IDBCreateSession,  
                                    (void**) &pIDBCreateSession)))  
        {  
            cout << "Failed to obtain IDBCreateSession interface.\n";  
        }  
  
        if(FAILED(pIDBCreateSession->CreateSession(  
                                         NULL,   
                                         IID_IDBCreateCommand,   
                                         (IUnknown**) &pIDBCreateCommand)))  
        {  
            cout << "pIDBCreateSession->CreateSession failed.\n";  
        }  
  
        // Access the ICommand interface.  
        if(FAILED(pIDBCreateCommand->CreateCommand(  
                                        NULL,   
                                        IID_ICommand,   
                                        (IUnknown**) &pICommand)))  
        {  
            cout << "Failed to access ICommand interface.\n";  
        }  
  
       // Get an ICommandStream interface.  
       if(FAILED(pICommand->QueryInterface( IID_ICommandStream, (void**) &pICommandStream)))  
       {  
          cout << "Failed to get an ICommandStream interface.\n";  
       }  
  
       // Get an ICommandProperties interface.  
       if(FAILED(pICommand->QueryInterface( IID_ICommandProperties, (void**) &pICommandProperties)))  
       {  
          cout << "Failed to get an ICommandProperties interface.\n";  
       }  
  
       // Set the command properties.  
       SetCommandProperties();  
  
        // Use SetCommandStream() to specify the command stream.  
        if(FAILED(pICommandStream->SetCommandStream(IID_ISequentialStream, DBGUID_DEFAULT, (ISequentialStream*) &XMLInput )))  
        {  
            cout << "Failed to set command stream.\n";  
        }  
  
        // Execute the command.  
        if(FAILED(hr = pICommand->Execute(NULL,   
                                        IID_ISequentialStream,   
                                        NULL,   
                                        &cNumRows,   
                                        (IUnknown **) &pIXMLOutput )))  
        {  
            cout << "Failed to execute command.\n";  
        }  
  
        // Process the result set.  
        ProcessResultSet();   
  
        // Free memory.  
       if( pIXMLOutput )  
          pIXMLOutput->Release();  
       pICommandProperties->Release();  
       pICommandStream->Release();  
        pICommand->Release();  
        pIDBCreateCommand->Release();  
        pIDBCreateSession->Release();  
  
        if(FAILED(pIDBInitialize->Uninitialize()))  
        {  
            /*Uninitialize is not required, but it fails if an interface  
            has not been released. This can be used for debugging.  
            cout << "Problem uninitializing.\n"; */  
        } // endif.  
        pIDBInitialize->Release();  
  
        // Release the COM library.  
        CoUninitialize();  
    };  
  
    //--------------------------------------------------------------------  
    void InitializeAndEstablishConnection()  
    {      
        // Initialize the COM library.  
        CoInitialize(NULL);  
  
        // Obtain access to the SQLOLEDB Provider.  
        hr = CoCreateInstance(CLSID_SQLOLEDB,   
                              NULL,   
                              CLSCTX_INPROC_SERVER,  
                              IID_IDBInitialize,   
                              (void **) &pIDBInitialize);  
        if(FAILED(hr))  
        {  
            printf("Failed to get IDBInitialize interface.\n");  
        } // end if  
  
        /*  
        Initialize the property values needed   
        to establish the connection.  
        */  
        for(i = 0; i < 4; i++)   
            VariantInit(&InitProperties[i].vValue);  
  
        // Server name.  
        InitProperties[0].dwPropertyID  = DBPROP_INIT_DATASOURCE;  
        InitProperties[0].vValue.vt     = VT_BSTR;  
        InitProperties[0].vValue.bstrVal=   
                                SysAllocString(L"Server");  
        InitProperties[0].dwOptions     = DBPROPOPTIONS_REQUIRED;  
        InitProperties[0].colid         = DB_NULLID;  
  
    // Database.  
        InitProperties[1].dwPropertyID  = DBPROP_INIT_CATALOG;  
        InitProperties[1].vValue.vt     = VT_BSTR;  
        InitProperties[1].vValue.bstrVal= SysAllocString(L"northwind");  
        InitProperties[1].dwOptions     = DBPROPOPTIONS_REQUIRED;  
        InitProperties[1].colid         = DB_NULLID;  
  
    // Username (login).  
        InitProperties[2].dwPropertyID  = DBPROP_AUTH_USERID;   
        InitProperties[2].vValue.vt     = VT_BSTR;  
        InitProperties[2].vValue.bstrVal= SysAllocString(L"Login");  
        InitProperties[2].dwOptions     = DBPROPOPTIONS_REQUIRED;  
        InitProperties[2].colid         = DB_NULLID;  
  
    // Password.  
    //    InitProperties[3].dwPropertyID  = DBPROP_AUTH_PASSWORD;   
    //    InitProperties[3].vValue.vt     = VT_BSTR;  
    //    InitProperties[3].vValue.bstrVal= SysAllocString(L"Password");  
    //    InitProperties[3].dwOptions     = DBPROPOPTIONS_REQUIRED;  
    //    InitProperties[3].colid         = DB_NULLID;  
  
        /*  
        Now that the properties are set, construct the DBPROPSET structure.  
        (rgInitPropSet). The DBPROPSET structure is used to pass an array   
        of DBPROP structures (InitProperties) to the SetProperties method.  
        */  
        rgInitPropSet[0].guidPropertySet = DBPROPSET_DBINIT;  
    //  rgInitPropSet[0].cProperties    = 4;  
        rgInitPropSet[0].cProperties    = 3;  
        rgInitPropSet[0].rgProperties   = InitProperties;  
  
        // Set initialization properties.  
        hr = pIDBInitialize->QueryInterface(IID_IDBProperties,   
                                       (void **)&pIDBProperties);  
        if(FAILED(hr))  
        {  
            cout << "Failed to get IDBProperties interface.\n";  
        }  
  
        hr = pIDBProperties->SetProperties(1, rgInitPropSet);   
        if(FAILED(hr))  
        {  
            cout << "Failed to set initialization properties.\n";  
        } // end if  
  
        pIDBProperties->Release();  
  
        // Establish the connection to the data source.  
        if(FAILED(pIDBInitialize->Initialize()))  
        {  
            cout << "Problem establishing connection to the data source.\n";  
        }  
    } // End of InitializeAndEstablishConnection.  
    void SetCommandProperties()  
    {      
    //    for(i = 0; i < 4; i++)   
            VariantInit(&InitProperties[0].vValue);  
  
        // Server name.  
        InitProperties[0].dwPropertyID  = SSPROP_STREAM_BASEPATH;  
        InitProperties[0].vValue.vt     = VT_BSTR;  
        InitProperties[0].vValue.bstrVal=   
                                SysAllocString(L"C:\\MyDir");  
        InitProperties[0].dwOptions     = DBPROPOPTIONS_REQUIRED;  
        InitProperties[0].colid         = DB_NULLID;  
  
        /*  
        Now that the properties are set, construct the DBPROPSET structure  
        (rgInitPropSet). The DBPROPSET structure is used to pass an array   
        of DBPROP structures (InitProperties) to the SetProperties method.  
        */  
        rgInitPropSet[0].guidPropertySet = DBPROPSET_SQLSERVERSTREAM;  
        rgInitPropSet[0].cProperties    = 1;  
        rgInitPropSet[0].rgProperties   = InitProperties;  
  
        // Set initialization properties.  
        hr = pICommandProperties->SetProperties(1, rgInitPropSet);   
        if(FAILED(hr))  
        {  
            cout << "Failed to set command properties.\n";  
        } // end if  
    } // End of InitializeAndEstablishConnection.  
  
    //--------------------------------------------------------------------  
    // Retrieve and display data resulting from a query.  
    void ProcessResultSet()  
    {  
       CHAR   szBuf[1000];  
       ULONG   ulNumRead;  
       HRESULT   hr;  
  
       if( pIXMLOutput == NULL )  
          return;  
  
       // Read from the stream.  
       ZeroMemory( szBuf, 1000 );  
       while( ( hr = pIXMLOutput->Read( szBuf, 1000, &ulNumRead ) ) == S_OK )  
       {  
          cout << szBuf;  
       }  
    } // Process resultset.  
    ```  
  
#### <a name="passing-parameters-to-templates"></a>템플릿에 매개 변수 전달  
 이 예에서는 매개 변수 값을 XML 명령에 전달하는 방법을 보여 줍니다. 이 XML 템플릿은 명령으로 지정됩니다.  
  
```  
<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<sql:header><sql:param name='Title'>Mr.</sql:param></sql:header>  
<sql:query>SELECT TOP 20 * FROM Person.Contact  
WHERE Title = @Title  
FOR XML AUTO</sql:query>  
</ROOT>  
```  
  
 템플릿에는 SQL 쿼리가 들어 있습니다. 쿼리 매개 변수 값이 필요 (@Title). 매개 변수 값을 전달하지 않으면 기본값("Mr.")이 사용됩니다.  
  
 매개 변수 값을 템플릿에 전달하는 경우 매개 변수 이름과 값을 모두 지정해야 합니다.  
  
 코드는 다음과 같습니다.  
  
```  
#define UNICODE  
#define _UNICODE  
#define DBINITCONSTANTS  
#define INITGUID  
  
#include <stdio.h>  
#include <tchar.h>  
#include <stddef.h>  
#include <windows.h>  
#include <iostream.h>  
#include "oledb.h"  
#include "SQLOLEDB.h"  
  
HRESULT InitializeAndEstablishConnection(IDBInitialize ** ppIDBInitialize);  
HRESULT SetCommandProperties(ICommand * pICommand);  
HRESULT ProcessResultSet(ISequentialStream * pStreamOutput);  
  
//---------------------------------------------------------------------  
// Structure Definition Section  
//---------------------------------------------------------------------  
struct COLUMNDATA  
{  
    DBLENGTH    dwLength;   // The length of the data field  
    DBSTATUS    dwStatus;   // The status value  
    BYTE        bData[1];   // The start of the data field  
};  
  
class CSequentialStream : public ISequentialStream  
{  
    private:      
        ULONG       m_cRef;             // reference count  
        HANDLE      m_hFile;            // handle to the file  
        LPWSTR      m_wszFileName;      // the file name  
  
    public:  
        CSequentialStream( LPWSTR );  
        virtual ~CSequentialStream();  
  
        // IUnknown Methods  
        STDMETHODIMP_(ULONG)    AddRef();  
        STDMETHODIMP_(ULONG)    Release();  
        STDMETHODIMP QueryInterface( REFIID, LPVOID* );  
  
        // ISequentialStream Methods  
        STDMETHODIMP Read(   
                /* [out] */ void __RPC_FAR*,  
                /* [in]  */ ULONG,  
                /* [out] */ ULONG __RPC_FAR* );  
  
        STDMETHODIMP Write(   
                /* [in] */ const void __RPC_FAR*,  
                /* [in] */ ULONG,  
                /* [out]*/ ULONG __RPC_FAR* );  
};  
  
CSequentialStream::CSequentialStream  
(  
    LPWSTR      wszFileName  
)  
:  
    m_cRef( 0 ),  
    m_hFile( NULL ),  
    m_wszFileName( NULL )  
{  
    // The constructor AddRefs.  
    AddRef();  
  
    // Allocate memory for the file name.  
    m_wszFileName = (LPWSTR) CoTaskMemAlloc( ( wcslen( wszFileName ) + 1 ) * 2 );  
  
    // Copy the file name  
    wcscpy( m_wszFileName, wszFileName );  
}  
  
CSequentialStream::~CSequentialStream  
(  
)  
{  
    // Free any allocated memory.  
    if( m_wszFileName )  
        CoTaskMemFree( m_wszFileName );  
  
    // Close the file.  
    if( m_hFile )  
        CloseHandle( m_hFile );  
}  
  
ULONG      
CSequentialStream::AddRef  
(  
)  
{  
    return ++m_cRef;  
}  
ULONG CSequentialStream::Release()  
{  
    if(--m_cRef)  
        return m_cRef;  
  
    delete this;  
    return 0;  
}  
  
HRESULT CSequentialStream::QueryInterface  
(     
    REFIID riid,   
    void** ppv  
)  
{  
    *ppv = NULL;  
  
    if (riid == IID_IUnknown)  
        *ppv = this;  
  
    if (riid == IID_ISequentialStream)  
        *ppv = this;  
  
    if(*ppv)  
    {  
        ((IUnknown*)*ppv)->AddRef();  
        return S_OK;  
    }  
  
    return E_NOINTERFACE;  
}  
  
HRESULT CSequentialStream::Read  
(  
    void *pv,   
    ULONG cb,   
    ULONG* pcbRead  
)  
{  
    ULONG   cBytesRead = 0;  
  
    // Parameter checking.  
    if(pcbRead)  
        *pcbRead = 0;  
  
    if(!pv)  
        return STG_E_INVALIDPOINTER;  
  
    if(cb == 0)  
        return S_OK;  
  
    // Do we need to open the file?  
    if( m_hFile == NULL )  
    {  
        // Open the file.  
        m_hFile = CreateFile( m_wszFileName, GENERIC_READ, 0, NULL, OPEN_EXISTING, 0, NULL );  
  
        // If we failed to open the file, return E_FAIL.  
        if( m_hFile == INVALID_HANDLE_VALUE )  
            return E_FAIL;  
    }  
  
    // Clear the buffer.  
    ZeroMemory( pv, cb );  
  
    // Read cb bytes from the stream.  
    if( !ReadFile( m_hFile, pv, cb, &cBytesRead, NULL ) )  
        return E_FAIL;  
  
    // Inform the user how many bytes were read.  
    if( NULL != pcbRead )   
        *pcbRead = cBytesRead;  
  
    if(cb != cBytesRead)  
        return S_FALSE;   
  
    return S_OK;  
}  
  
HRESULT CSequentialStream::Write  
(  
    const void *pv,   
    ULONG cb,   
    ULONG* pcbWritten  
)  
{  
    // For purposes of this example, only a read-only stream is needed.  
    return STG_E_CANTSAVE;  
}  
void main()   
{  
    HRESULT                 hr = S_OK;  
    IDBInitialize         * pIDBInitialize          = NULL;  
    IDBCreateSession      * pIDBCreateSession       = NULL;  
    IDBCreateCommand      * pIDBCreateCommand       = NULL;  
    ICommand              * pICommand               = NULL;  
    ICommandStream        * pICommandStream         = NULL;  
    ICommandWithParameters* pICommandWithParameters = NULL;  
    ICommandText          * pICommandText           = NULL;  
    IAccessor             * pIAccessor              = NULL;  
    const ULONG             nParams = 1;  
    DBPARAMS              * pParams                 = NULL;  
    DBPARAMS                params;  
    DBBINDING               acDBBinding[nParams];  
    DBBINDSTATUS            acDBBindStatus[nParams];  
    DBORDINAL               rgParamOrdinals[1];  
    DBPARAMBINDINFO         rgParamBindInfo[1];  
    const WCHAR           * wszParamName =      L"@CategoryName";  
    const WCHAR           * wszDataSourceType = L"DBTYPE_WCHAR";  
    BYTE                    sprocparams[1000];  
    COLUMNDATA            * pCol = (COLUMNDATA *) sprocparams;  
    ISequentialStream     * pStreamOutput       = NULL;  
    DBCOLUMNINFO          * pDBColumnInfo       = NULL;  
    HACCESSOR               hAccessor;  
    CSequentialStream       XMLInput( L"TemplateFile.xml" );  
  
    typedef struct tagSPROCPARAMS  
    {  
        WCHAR CategoryName[25];  
    } SPROCPARAMS;  
  
    CoInitialize(0);  
  
    // Call a function to initialize and establish connection.   
    if (FAILED(hr = InitializeAndEstablishConnection(&pIDBInitialize)))  
        goto Cleanup;  
  
    //Create a session object.  
    if(FAILED(hr = pIDBInitialize->QueryInterface(  
                                IID_IDBCreateSession,  
                                (void**) &pIDBCreateSession)))  
    {  
        cout << "Failed to obtain IDBCreateSession interface.\n";  
        goto Cleanup;  
    }  
  
    if(FAILED(hr = pIDBCreateSession->CreateSession(  
                                     NULL,   
                                     IID_IDBCreateCommand,   
                                     (IUnknown**) &pIDBCreateCommand)))  
    {  
        cout << "pIDBCreateSession->CreateSession failed.\n";  
        goto Cleanup;  
    }  
  
    //Access the ICommand interface.  
    if(FAILED(hr = pIDBCreateCommand->CreateCommand(  
                                    NULL,   
                                    IID_ICommand,   
                                    (IUnknown**) &pICommand)))  
    {  
        cout << "Failed to access ICommand interface.\n";  
        goto Cleanup;  
    }  
  
    // Get an ICommandStream interface  
    if(FAILED(pICommand->QueryInterface( IID_ICommandStream, (void**) &pICommandStream)))  
    {  
        cout << "Failed to get an ICommandStream interface.\n";  
        goto Cleanup;  
    }  
  
    //Use SetCommandStream() to specify the command stream.  
    if(FAILED(hr = pICommandStream->SetCommandStream(IID_ISequentialStream, DBGUID_DEFAULT, (ISequentialStream*) &XMLInput )))  
    {  
        cout << "Failed to set command stream.\n";  
        goto Cleanup;  
    }  
  
    // Set the command properties.  
    if (FAILED(hr = SetCommandProperties(pICommand)))  
        goto Cleanup;  
  
    //***************************************  
    pCol->dwStatus = DBSTATUS_S_OK;  
    wcscpy( (LPWSTR) pCol->bData, L"Condiments" );  
    pCol->dwLength = wcslen( (LPWSTR) pCol->bData) * sizeof(WCHAR);  
  
    /*Describe the consumer buffer by filling in the array.   
    of DBBINDING structures.  Each binding associates  
    a single parameter to the consumer's buffer.*/  
    acDBBinding[0].iOrdinal     = 1;  
    acDBBinding[0].obLength     = offsetof( COLUMNDATA, dwLength );  
    acDBBinding[0].obStatus     = offsetof( COLUMNDATA, dwStatus );  
    acDBBinding[0].pTypeInfo    = NULL;  
    acDBBinding[0].pObject      = NULL;  
    acDBBinding[0].pBindExt     = NULL;  
    acDBBinding[0].dwPart       = DBPART_VALUE | DBPART_STATUS | DBPART_LENGTH;  
    acDBBinding[0].dwMemOwner   = DBMEMOWNER_CLIENTOWNED;  
    acDBBinding[0].dwFlags      = 0;  
    acDBBinding[0].bScale       = 0;  
    acDBBinding[0].obValue      = offsetof( COLUMNDATA, bData );  
    acDBBinding[0].eParamIO     = DBPARAMIO_INPUT;  
    acDBBinding[0].cbMaxLen     = 50;   
    acDBBinding[0].wType        = DBTYPE_WSTR;  
    acDBBinding[0].bPrecision   = 0;  
  
    rgParamOrdinals[0]              = 1;  
    rgParamBindInfo[0].bPrecision   = 0;  
    rgParamBindInfo[0].bScale       = 0;  
    rgParamBindInfo[0].dwFlags      = DBPARAMFLAGS_ISINPUT;  
    rgParamBindInfo[0].pwszDataSourceType = (WCHAR *)wszDataSourceType;  
    rgParamBindInfo[0].pwszName     = (WCHAR *)wszParamName;  
    rgParamBindInfo[0].ulParamSize  = 35;  
  
    if (FAILED(hr = pICommandStream->QueryInterface(  
                        IID_ICommandWithParameters,  
                        (LPVOID *)&pICommandWithParameters)))  
    {  
        cout << "Error.\n";  
        goto Cleanup;  
    }  
  
    if (FAILED(hr = pICommandWithParameters->SetParameterInfo(  
                        nParams,  
                        rgParamOrdinals,  
                        rgParamBindInfo)))  
    {  
        cout << "Error.\n";  
        goto Cleanup;  
    }  
  
    //Create an accessor from the above set of bindings.  
    if (FAILED(hr = pICommandStream->QueryInterface(  
                                    IID_IAccessor,   
                                    (void**)&pIAccessor)))  
    {  
        cout << "Failed to get IAccessor interface.\n";  
        goto Cleanup;  
    }  
  
    if (FAILED(hr = pIAccessor->CreateAccessor(  
                            DBACCESSOR_PARAMETERDATA,  
                            nParams,   
                            acDBBinding,   
                            sizeof(SPROCPARAMS),   
                            &hAccessor,  
                            acDBBindStatus)))  
    {  
        cout << "Failed to create accessor for the defined parameters.\n";  
        goto Cleanup;  
    }  
    /*  
    Fill in DBPARAMS structure for the command execution. This structure  
    specifies the parameter values in the command and is then passed   
    to Execute.  
    */  
    params.pData = sprocparams; //pCol->bData; //sprocparams;  
    params.cParamSets = 1;  
    params.hAccessor = hAccessor;  
  
    pParams = &params;  
  
    //***************************************  
    //Execute the command.  
    if(FAILED(hr = pICommand->Execute(NULL,   
                                    IID_ISequentialStream,   
                                    pParams,   
                                    NULL,   
                                    (IUnknown **) &pStreamOutput )))  
    {  
        cout << "Failed to execute command.\n";  
        goto Cleanup;  
    }  
  
    //Process the result set.  
    if (FAILED(hr = ProcessResultSet(pStreamOutput)))  
    {  
        goto Cleanup;  
    }  
  
Cleanup:  
    //Free up memory.  
    if( pStreamOutput )  
        pStreamOutput->Release();  
    if (pICommandStream)  
        pICommandStream->Release();  
    if (pICommand)  
        pICommand->Release();  
    if (pIDBCreateCommand)  
        pIDBCreateCommand->Release();  
    if (pIDBCreateSession)  
        pIDBCreateSession->Release();  
    if (pIDBInitialize)  
        pIDBInitialize->Release();  
  
    if (hr)  
    {  
        IErrorInfo* pErrorInfo = NULL;  
        BSTR        bstrDesc = NULL;  
        GetErrorInfo(0, &pErrorInfo);  
        if (pErrorInfo)  
        {  
            pErrorInfo->GetDescription(&bstrDesc);  
            printf ("\r\nError: %S\r\n", bstrDesc ? bstrDesc : L"Unknown error");  
            SysFreeString(bstrDesc);  
            pErrorInfo->Release();  
        }  
    }  
  
    //Release the COM library.  
    CoUninitialize();  
};  
  
//--------------------------------------------------------------------  
HRESULT InitializeAndEstablishConnection(IDBInitialize ** ppIDBInitialize)  
{  
    HRESULT         hr = S_OK;  
    IDBInitialize * pIDBInitialize = NULL;  
    IDBProperties * pIDBProperties = NULL;  
    DBPROP          rgIDBProps[4];  
    DBPROPSET       rgIDBPropSet[1];  
    int             ii;  
  
    if (!ppIDBInitialize)  
        return E_INVALIDARG;  
  
    *ppIDBInitialize = NULL;  
  
    /*  
    Initialize the property values needed   
    to establish the connection.  
    */  
    for(ii = 0; ii < 4; ii++)   
        VariantInit(&rgIDBProps[ii].vValue);  
  
    //Obtain access to the SQLOLEDB provider.  
    if(FAILED(hr = CoCreateInstance(CLSID_SQLOLEDB,   
                          NULL,   
                          CLSCTX_INPROC_SERVER,  
                          IID_IDBInitialize,   
                          (void **) &pIDBInitialize)))  
    {  
        printf("Failed to get IDBInitialize interface.\n");  
        goto Cleanup;  
    }  
  
    //Server name.  
    rgIDBProps[0].dwPropertyID  = DBPROP_INIT_DATASOURCE;  
    rgIDBProps[0].vValue.vt     = VT_BSTR;  
    rgIDBProps[0].vValue.bstrVal= SysAllocString(L"server");  
    rgIDBProps[0].dwOptions     = DBPROPOPTIONS_REQUIRED;  
    rgIDBProps[0].colid         = DB_NULLID;  
  
//Database.  
    rgIDBProps[1].dwPropertyID  = DBPROP_INIT_CATALOG;  
    rgIDBProps[1].vValue.vt     = VT_BSTR;  
    rgIDBProps[1].vValue.bstrVal= SysAllocString(L"Northwind");  
    rgIDBProps[1].dwOptions     = DBPROPOPTIONS_REQUIRED;  
    rgIDBProps[1].colid         = DB_NULLID;  
  
//User name (login).  
    rgIDBProps[2].dwPropertyID  = DBPROP_AUTH_USERID;   
    rgIDBProps[2].vValue.vt     = VT_BSTR;  
    rgIDBProps[2].vValue.bstrVal= SysAllocString(L"sa");  
    rgIDBProps[2].dwOptions     = DBPROPOPTIONS_REQUIRED;  
    rgIDBProps[2].colid         = DB_NULLID;  
  
//Password.  
//    rgIDBProps[3].dwPropertyID  = DBPROP_AUTH_PASSWORD;   
//    rgIDBProps[3].vValue.vt     = VT_BSTR;  
//    rgIDBProps[3].vValue.bstrVal= SysAllocString(L"password");  
//    rgIDBProps[3].dwOptions     = DBPROPOPTIONS_REQUIRED;  
//    rgIDBProps[3].colid         = DB_NULLID;  
  
    /*  
    Now that the properties are set, construct the DBPROPSET structure  
    (rgInitPropSet). The DBPROPSET structure is used to pass an array   
    of DBPROP structures (rgIDBProps) to the SetProperties method.  
    */  
    rgIDBPropSet[0].guidPropertySet = DBPROPSET_DBINIT;  
//  rgInitPropSet[0].cProperties    = 4;  
    rgIDBPropSet[0].cProperties    = 3;  
    rgIDBPropSet[0].rgProperties   = rgIDBProps;  
  
    //Set initialization properties.  
    if (FAILED(hr = pIDBInitialize->QueryInterface(IID_IDBProperties,   
                                   (void **)&pIDBProperties)))  
    {  
        cout << "Failed to get IDBProperties interface.\n";  
        goto Cleanup;  
    }  
  
    if (FAILED(hr = pIDBProperties->SetProperties(1, rgIDBPropSet)))  
    {  
        cout << "Failed to set initialization properties.\n";  
        goto Cleanup;  
    } //end if  
  
    //Now establish the connection to the data source.  
    if(FAILED(hr = pIDBInitialize->Initialize()))  
    {  
        cout << "Problem in establishing connection to the data source.\n";  
        goto Cleanup;  
    }  
  
    *ppIDBInitialize = pIDBInitialize;  
  
Cleanup:  
    for(ii = 0; ii < 4; ii++)   
        VariantClear(&rgIDBProps[ii].vValue);  
  
    if (pIDBProperties)  
        pIDBProperties->Release();  
    return hr;  
} //End of InitializeAndEstablishConnection.  
  
HRESULT SetCommandProperties(ICommand * pICommand)  
{  
    HRESULT     hr = S_OK;  
    DBPROP      rgProps[1];  
    DBPROPSET   rgPropSet[1];  
    ICommandProperties* pICommandProperties = NULL;  
  
    VariantInit(&rgProps[0].vValue);  
  
    //Server name.  
    rgProps[0].dwPropertyID  = SSPROP_STREAM_BASEPATH;  
    rgProps[0].vValue.vt     = VT_BSTR;  
    rgProps[0].vValue.bstrVal= SysAllocString(L"D:\\Test");  
    rgProps[0].dwOptions     = DBPROPOPTIONS_REQUIRED;  
    rgProps[0].colid         = DB_NULLID;  
  
    /*  
    Now that the properties are set, construct the DBPROPSET structure  
    (rgInitPropSet). The DBPROPSET structure is used to pass an array   
    of DBPROP structures (rgProps) to the SetProperties method.  
    */  
    rgPropSet[0].guidPropertySet = DBPROPSET_SQLSERVERSTREAM;  
    rgPropSet[0].cProperties    = 1;  
    rgPropSet[0].rgProperties   = rgProps;  
  
    // Get an ICommandProperties interface.  
    if(FAILED(pICommand->QueryInterface( IID_ICommandProperties, (void**) &pICommandProperties)))  
    {  
        cout << "Failed to get an ICommandProperties interface.\n";  
        goto Cleanup;  
    }  
  
    //Set initialization properties.  
    if(FAILED(hr = pICommandProperties->SetProperties(1, rgPropSet)))  
    {  
        cout << "Failed to set command properties.\n";  
        goto Cleanup;  
    }  
Cleanup:  
    VariantClear(&rgProps[0].vValue);  
    if (pICommandProperties)  
        pICommandProperties->Release();  
    return hr;  
}  
  
//--------------------------------------------------------------------  
//Retrieve and display data resulting from a query.  
HRESULT ProcessResultSet(ISequentialStream * pStreamOutput)  
{  
    CHAR    szBuf[1000];  
    ULONG   ulNumRead;  
    HRESULT hr;  
  
    if( pStreamOutput == NULL )  
        return E_INVALIDARG;  
  
    // Read from the stream  
    ZeroMemory( szBuf, 1000 );  
    while( ( hr = pStreamOutput->Read( szBuf, 1000, &ulNumRead ) ) == S_OK )  
    {  
        cout << szBuf;  
        cout.flush();  
    }  
    return hr;  
} //ProcessResultSet.  
```  
  
  
