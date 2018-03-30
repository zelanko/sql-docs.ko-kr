---
title: 데이터 원본 개체 (OLE DB) | Microsoft Docs
description: 데이터 원본 개체(OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b1fd12d353e5c7ecc47852ea1ab570694312df1f
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2018
---
# <a name="data-source-objects-ole-db"></a>데이터 원본 개체(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB Driver for SQL Server와 같은 데이터 저장소에 대 한 링크를 설정 하는 데 사용 되는 OLE DB 인터페이스 집합에 대 한 데이터 원본 이라는 용어를 사용 하 여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. 공급자의 데이터 원본 개체의 인스턴스를 만들기는 OLE DB Driver for SQL Server 소비자의 첫 번째 작업입니다.  
  
 각 OLE DB 공급자는 자체적으로 사용할 CLSID(클래스 식별자)를 선언합니다. OLE DB Driver for SQL Server에 대 한 CLSID는 C/c + + GUID CLSID_MSOLEDBSQL (MSOLEDBSQL_CLSID 올바른로 확인 되는 기호 참조 하는 msoledbsql.h 파일에 progid). CLSID를 소비자에서 사용 하 여 OLE **CoCreateInstance** 함수를 데이터 원본 개체의 인스턴스를 제조 합니다.  
  
 OLE DB Driver for SQL Server가 프로세스 서버입니다. SQL Server 개체에 대 한 OLE DB Driver의 인스턴스는 실행 컨텍스트를 나타내기 위해 위해 CLSCTX_INPROC_SERVER 매크로 사용 하 여 만들어집니다.  
  
 OLE DB 드라이버에서 SQL Server 데이터 원본 개체를 변경할 수 있도록 기존 클러스터에 연결 하는 OLE DB 초기화 인터페이스 노출 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스.  
  
 SQL Server 용 OLE DB 드라이버를 통해 만든 모든 연결이 이러한 옵션을 자동으로 설정 합니다.  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 이 예제에서는 클래스 식별자 매크로 사용 하 여 SQL Server 데이터 원본 개체에 대 한 참조를 가져올에 대 한 OLE DB 드라이버를 만들려는 해당 **IDBInitialize** 인터페이스입니다.  
  
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
  
 성공적으로 만들어지면은 OLE DB Driver for SQL Server 데이터 원본 개체의 인스턴스를 소비자 응용 프로그램에서는 데이터 원본을 초기화 하 고 세션을 만들어 여 계속할 수 있습니다. OLE DB 세션은 데이터 액세스 및 조작을 가능하게 하는 인터페이스를 제공합니다.  
  
 OLE DB Driver for SQL Server의 지정 된 인스턴스에 처음 연결 하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 성공적인 데이터 원본 초기화의 일부로 합니다. 연결이 때까지 또는 모든 데이터 원본 초기화 인터페이스에 대 한 참조를 유지 관리 되는 그대로 유지 되는 **idbinitialize:: Uninitialize** 메서드를 호출 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [데이터 원본 속성 &#40; OLE db&#41;](../../oledb/ole-db-data-source-objects/data-source-properties-ole-db.md)  
  
-   [데이터 원본 정보 속성](../../oledb/ole-db-data-source-objects/data-source-information-properties.md)  
  
-   [초기화 및 권한 부여 속성](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md)  
  
-   [세션](../../oledb/ole-db-data-source-objects/sessions.md)  
  
-   [세션 속성-OLE DB Driver for SQL Server](../../oledb/ole-db-data-source-objects/session-properties-oledb-driver-for-sql-server.md)  
  
-   [지속형 데이터 원본 개체](../../oledb/ole-db-data-source-objects/persisted-data-source-objects.md)  
  
## <a name="see-also"></a>관련 항목:  
 [OLE DB Driver for SQL Server &#40;OLE DB&#41;](../../oledb/ole-db/oledb-driver-for-sql-server-ole-db.md)  
  
  
