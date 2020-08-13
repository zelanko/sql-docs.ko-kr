---
title: 데이터 원본에 대한 연결 설정(OLE DB 드라이버) | Microsoft Docs
description: OLE DB Driver for SQL Server를 사용하여 데이터 원본에 대한 연결 설정
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data sources [OLE DB Driver for SQL Server]
- connections [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, data source connections
- CoCreateInstance method
- OLE DB data sources [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 79f0ba6da0416c269d4a23cf45862746462f38e4
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87244842"
---
# <a name="establishing-a-connection-to-a-data-source"></a>데이터 원본에 대한 연결 설정
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server용 OLE DB 드라이버에 액세스하려면 소비자는 먼저 **CoCreateInstance** 메서드를 호출하여 데이터 원본 개체의 인스턴스를 만들어야 합니다. 각 OLE DB 공급자는 고유한 CLSID(클래스 ID)를 사용하여 식별합니다. OLE DB Driver for SQL Server의 경우 클래스 식별자는 CLSID_MSOLEDBSQL입니다. 참조하는 msoledbsql.h에서 사용되는 OLE DB Driver for SQL Server로 확인되는 기호 MSOLEDBSQL_CLSID를 사용할 수도 있습니다.  
  
 소비자는 데이터 원본 개체가 공개하는 **IDBProperties** 인터페이스를 사용하여 서버 이름, 데이터베이스 이름, 사용자 ID 및 암호와 같은 기본 인증 정보를 제공할 수 있습니다. 이러한 속성을 설정하려면 **IDBProperties::SetProperties** 메서드를 호출합니다.  
  
 컴퓨터에서 여러 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 실행되는 경우 서버 이름은 ServerName\InstanceName 형식으로 지정됩니다.  
  
 데이터 원본 개체는 또한 **IDBInitialize** 인터페이스를 공개합니다. 속성을 설정한 다음에는 **IDBInitialize::Initialize** 메서드를 호출하여 데이터 원본에 연결할 수 있습니다. 다음은 그 예입니다.  
  
```cpp
CoCreateInstance(CLSID_MSOLEDBSQL,   
                 NULL,   
                 CLSCTX_INPROC_SERVER,  
                 IID_IDBInitialize,   
                 (void **) &pIDBInitialize)  
```
  
 이렇게 **CoCreateInstance**를 호출하면 CLSID_MSOLEDBSQL(개체를 만드는 데 사용되는 데이터 및 코드와 연관된 CLSID)과 연관된 클래스의 단일 개체가 생성됩니다. IID_IDBInitialize는 개체와 통신하는 데 사용되는 인터페이스(**IDBInitialize**)의 식별자에 대한 참조입니다.  
  
 다음 샘플은 데이터 원본에 대한 연결을 시작하고 설정하는 방법을 보여줍니다.
  
```cpp
#include "msoledbsql.h"
#include <stdio.h>

HRESULT InitializeAndEstablishConnection(IDBInitialize *&pIDBInitialize);

void main() {
    IDBInitialize       *pIDBInitialize = nullptr;
    HRESULT             hr = S_OK;

    // Initialize The Component Object Module Library
    CoInitialize(nullptr);

    hr = InitializeAndEstablishConnection(pIDBInitialize);
    if (FAILED(hr)) {
        printf("Failed to establish connection.\r\n");
        goto _ExitMain;
    }

    // Insert code that uses the established connection

_ExitMain:
    // Free Up All Allocated Memory
    if (pIDBInitialize)
    {
        pIDBInitialize->Uninitialize();
        pIDBInitialize->Release();
        pIDBInitialize = nullptr;
    }

    // Release The Component Object Module Library
    CoUninitialize();
}

HRESULT InitializeAndEstablishConnection(IDBInitialize *&pIDBInitialize) {
    IDBProperties   *pIDBProperties = nullptr;
    DBPROP          InitProperties[3] = { 0 };
    DBPROPSET       rgInitPropSet[1] = { 0 };
    HRESULT         hr = S_OK;

    // Obtain access to the OLE DB Driver for SQL Server.  
    hr = CoCreateInstance(CLSID_MSOLEDBSQL,
                          NULL,
                          CLSCTX_INPROC_SERVER,
                          IID_IDBInitialize,
                          (void **)&pIDBInitialize);
    if (FAILED(hr)) {
        printf("Failed to obtain access to the OLE DB Driver.\r\n");
        goto _ExitInitialize;
    }
    // Initialize property values needed to establish connection.  
    for (int i = 0; i < 3; i++) {
        VariantInit(&InitProperties[i].vValue);
    }

    // Server name.  
    // See DBPROP structure for more information on InitProperties  
    InitProperties[0].dwPropertyID = DBPROP_INIT_DATASOURCE;
    InitProperties[0].vValue.vt = VT_BSTR;
    InitProperties[0].vValue.bstrVal = SysAllocString(L"Server");
    InitProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;
    InitProperties[0].colid = DB_NULLID;

    // Database.  
    InitProperties[1].dwPropertyID = DBPROP_INIT_CATALOG;
    InitProperties[1].vValue.vt = VT_BSTR;
    InitProperties[1].vValue.bstrVal = SysAllocString(L"database");
    InitProperties[1].dwOptions = DBPROPOPTIONS_REQUIRED;
    InitProperties[1].colid = DB_NULLID;

    // Username (login).  
    InitProperties[2].dwPropertyID = DBPROP_AUTH_INTEGRATED;
    InitProperties[2].vValue.vt = VT_BSTR;
    InitProperties[2].vValue.bstrVal = SysAllocString(L"SSPI");
    InitProperties[2].dwOptions = DBPROPOPTIONS_REQUIRED;
    InitProperties[2].colid = DB_NULLID;

    // Construct the DBPROPSET structure(rgInitPropSet). The   
    // DBPROPSET structure is used to pass an array of DBPROP   
    // structures (InitProperties) to the SetProperties method.  
    rgInitPropSet[0].guidPropertySet = DBPROPSET_DBINIT;
    rgInitPropSet[0].cProperties = 3;
    rgInitPropSet[0].rgProperties = InitProperties;

    // Set initialization properties.  
    hr = pIDBInitialize->QueryInterface(IID_IDBProperties,
                                        (void **)&pIDBProperties);
    if (FAILED(hr)) {
        printf("Failed to obtain an IDBProperties interface.\r\n");
        goto _ExitInitialize;
    }
    hr = pIDBProperties->SetProperties(1, rgInitPropSet);
    if (FAILED(hr)) {
        printf("Failed to set initialization properties.\r\n");
        goto _ExitInitialize;
    }

    // Now establish the connection to the data source.  
    hr = pIDBInitialize->Initialize();
    if (FAILED(hr)) {
        printf("Failed to establish connection with the server.\r\n");
        goto _ExitInitialize;
    }

_ExitInitialize:
    if (pIDBProperties)
    {
        pIDBProperties->Release();
        pIDBProperties = nullptr;
    }

    if (FAILED(hr))
    {
        if (pIDBInitialize)
        {
            pIDBInitialize->Release();
            pIDBInitialize = nullptr;
        }
    }

    return hr;
}
```  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 애플리케이션용 OLE DB 드라이버 만들기](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)  
  
  
