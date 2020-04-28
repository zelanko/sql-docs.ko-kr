---
title: 데이터 원본에 대한 연결 설정 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data sources [SQL Server Native Client]
- connections [SQL Server Native Client]
- SQL Server Native Client OLE DB provider, data source connections
- CoCreateInstance method
- OLE DB data sources [SQL Server Native Client]
ms.assetid: 7ebd1394-cc8d-4bcf-92f3-c374a26e7ba0
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e4ec6125d3c8fe2469f599b3f11c1888383de6e5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81290479"
---
# <a name="establishing-a-connection-to-a-data-source"></a>데이터 원본에 대한 연결 설정
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에 액세스 하려면 소비자는 먼저 **CoCreateInstance** 메서드를 호출 하 여 데이터 원본 개체의 인스턴스를 만들어야 합니다. 각 OLE DB 공급자는 고유한 CLSID(클래스 ID)를 사용하여 식별합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자의 경우 클래스 식별자가 CLSID_SQLNCLI10 됩니다. 참조 하는 SQLNCLI에서 사용 되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 확인 하는 SQLNCLI_CLSID 기호를 사용할 수도 있습니다.  
  
 소비자는 데이터 원본 개체가 공개하는 **IDBProperties** 인터페이스를 사용하여 서버 이름, 데이터베이스 이름, 사용자 ID 및 암호와 같은 기본 인증 정보를 제공할 수 있습니다. 이러한 속성을 설정하려면 **IDBProperties::SetProperties** 메서드를 호출합니다.  
  
 컴퓨터에서 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 실행되는 경우 서버 이름은 ServerName\InstanceName 형식으로 지정됩니다.  
  
 데이터 원본 개체는 또한 **IDBInitialize** 인터페이스를 공개합니다. 속성을 설정한 다음에는 **IDBInitialize::Initialize** 메서드를 호출하여 데이터 원본에 연결할 수 있습니다. 예를 들면 다음과 같습니다.  
  
```  
CoCreateInstance(CLSID_SQLNCLI10,   
                 NULL,   
                 CLSCTX_INPROC_SERVER,  
                 IID_IDBInitialize,   
                 (void **) &pIDBInitialize)  
```  
  
 이 **CoCreateInstance** 호출은 CLSID_SQLNCLI10와 연결 된 클래스의 단일 개체 (데이터와 연결 된 CSLID 개체를 만드는 데 사용 되는 코드)를 만듭니다. IID_IDBInitialize는 개체와 통신하는 데 사용되는 인터페이스(**IDBInitialize**)의 식별자에 대한 참조입니다.  
  
 다음 예제 함수는 데이터 원본에 대한 연결을 초기화하고 설정합니다.  
  
```  
void InitializeAndEstablishConnection() {  
   // Initialize the COM library.  
   CoInitialize(NULL);  
  
   // Obtain access to the SQL Server Native Client OLE DB provider.  
   hr = CoCreateInstance(CLSID_SQLNCLI10,   
                         NULL,   
                         CLSCTX_INPROC_SERVER,  
                         IID_IDBInitialize,   
                         (void **) &pIDBInitialize);  
   // Initialize property values needed to establish connection.  
   for (i = 0 ; i < 4 ; i++)   
      VariantInit(&InitProperties[i].vValue);  
  
   // Server name.  
   // See DBPROP structure for more information on InitProperties  
   InitProperties[0].dwPropertyID  = DBPROP_INIT_DATASOURCE;  
   InitProperties[0].vValue.vt    = VT_BSTR;  
   InitProperties[0].vValue.bstrVal=   
                     SysAllocString(L"Server");  
   InitProperties[0].dwOptions    = DBPROPOPTIONS_REQUIRED;  
   InitProperties[0].colid       = DB_NULLID;  
  
   // Database.  
   InitProperties[1].dwPropertyID  = DBPROP_INIT_CATALOG;  
   InitProperties[1].vValue.vt    = VT_BSTR;  
   InitProperties[1].vValue.bstrVal= SysAllocString(L"database");  
   InitProperties[1].dwOptions    = DBPROPOPTIONS_REQUIRED;  
   InitProperties[1].colid       = DB_NULLID;  
  
   // Username (login).  
   InitProperties[2].dwPropertyID  = DBPROP_AUTH_INTEGRATED;  
   InitProperties[2].vValue.vt    = VT_BSTR;  
   InitProperties[2].vValue.bstrVal= SysAllocString(L"SSPI");  
   InitProperties[2].dwOptions    = DBPROPOPTIONS_REQUIRED;  
   InitProperties[2].colid       = DB_NULLID;  
   InitProperties[3].dwOptions    = DBPROPOPTIONS_REQUIRED;  
   InitProperties[3].colid       = DB_NULLID;  
  
   // Construct the DBPROPSET structure(rgInitPropSet). The   
   // DBPROPSET structure is used to pass an array of DBPROP   
   // structures (InitProperties) to the SetProperties method.  
   rgInitPropSet[0].guidPropertySet = DBPROPSET_DBINIT;  
   rgInitPropSet[0].cProperties   = 4;  
   rgInitPropSet[0].rgProperties   = InitProperties;  
  
   // Set initialization properties.  
   hr = pIDBInitialize->QueryInterface(IID_IDBProperties,   
                           (void **)&pIDBProperties);  
   hr = pIDBProperties->SetProperties(1, rgInitPropSet);   
   pIDBProperties->Release();  
  
   // Now establish the connection to the data source.  
   pIDBInitialize->Initialize();  
}  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client OLE DB 공급자 애플리케이션 만들기](../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
  
