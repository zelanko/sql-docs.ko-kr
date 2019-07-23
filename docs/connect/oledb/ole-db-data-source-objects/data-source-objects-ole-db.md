---
title: 데이터 원본 개체 (OLE DB) | Microsoft Docs
description: 데이터 원본 개체(OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], data source objects
- OLE DB Driver for SQL Server, data source objects
- MSOLEDBSQL, data source objects
- OLE DB Driver for SQL Server, data source objects
- OLE DB data source objects [OLE DB Driver for SQL Server]
- data source objects [OLE DB]
- CLSID
author: pmasl
ms.author: pelopes
ms.openlocfilehash: e0394c5fd3b72c538904c9b8cf946316e76e6650
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015917"
---
# <a name="data-source-objects-ole-db"></a>데이터 원본 개체(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server용 OLE DB 드라이버에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 같은 데이터 저장소에 연결할 때 사용되는 OLE DB 인터페이스 집합에 데이터 원본이라는 용어를 사용합니다. 공급자의 데이터 원본 개체의 인스턴스를 만드는 것은 SQL Server 소비자에 대 한 OLE DB 드라이버의 첫 번째 작업입니다.  
  
 각 OLE DB 공급자는 자체적으로 사용할 CLSID(클래스 식별자)를 선언합니다. SQL Server에 대 한 OLE DB 드라이버의 CLSID는 C/C++ GUID CLSID_MSOLEDBSQL (기호 MSOLEDBSQL_CLSID는 참조 하는 MSOLEDBSQL 파일의 올바른 progid로 확인 됨). CLSID가 있으면 소비자는 OLE **CoCreateInstance** 함수를 사용하여 데이터 원본 개체의 인스턴스를 만듭니다.  
  
 SQL Server에 대 한 OLE DB 드라이버는 in-process 서버입니다. SQL Server용 OLE DB 드라이버 개체의 인스턴스는 실행 가능 콘텐츠를 나타내기 위해 CLSCTX_INPROC_SERVER 매크로를 사용하여 만들어집니다.  
  
 SQL Server용 OLE DB 드라이버 데이터 원본 개체는 소비자가 기존 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 데 사용할 수 있는 OLE DB 초기화 인터페이스를 노출합니다.  
  
 SQL Server에 대 한 OLE DB 드라이버를 통해 수행 된 모든 연결은 자동으로 다음 옵션을 설정 합니다.  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 이 예에서는 클래스 식별자 매크로를 사용하여 SQL Server용 OLE DB 드라이버 데이터 원본 개체를 만들고 **IDBInitialize** 인터페이스에 대한 참조를 가져옵니다.  
  
```  
IDBInitialize*   pIDBInitialize;  
HRESULT          hr;  
  
hr = CoCreateInstance(CLSID_MSOLEDBSQL, NULL, CLSCTX_INPROC_SERVER,  
    IID_IDBInitialize, (void**) &pIDBInitialize);  
  
if (SUCCEEDED(hr))  
{  
    //  Perform necessary processing with the interface.  
    pIDBInitialize->Uninitialize();  
    pIDBInitialize->Release();  
}  
else  
{  
    // Display error from CoCreateInstance.  
}  
```  
  
 SQL Server용 OLE DB 드라이버 데이터 원본 개체의 인스턴스가 성공적으로 만들어지면 소비자 애플리케이션에서는 데이터 원본을 초기화하고 세션을 만들어 작업을 계속할 수 있습니다. OLE DB 세션은 데이터 액세스 및 조작을 가능하게 하는 인터페이스를 제공합니다.  
  
 데이터 원본이 성공적으로 초기화되면SQL Server용 OLE DB 드라이버는 초기화의 일부로 지정된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 처음 연결합니다. 이 연결은 데이터 원본 초기화 인터페이스에 대한 참조가 유지되는 동안이나 **IDBInitialize::Uninitialize** 메서드가 호출될 때까지 유지됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [데이터 원본 속성&#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-properties-ole-db.md)  
  
-   [데이터 원본 정보 속성](../../oledb/ole-db-data-source-objects/data-source-information-properties.md)  
  
-   [초기화 및 권한 부여 속성](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md)  
  
-   [세션](../../oledb/ole-db-data-source-objects/sessions.md)  
  
-   [세션 속성 - SQL Server용 OLE DB 드라이버](../../oledb/ole-db-data-source-objects/session-properties-oledb-driver-for-sql-server.md)  
  
-   [지속형 데이터 원본 개체](../../oledb/ole-db-data-source-objects/persisted-data-source-objects.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 프로그래밍용 OLE DB 드라이버](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
