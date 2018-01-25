---
title: "데이터 원본 개체 (OLE DB) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-data-source-objects
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], data source objects
- SQL Server Native Client, data source objects
- SQLNCLI, data source objects
- SQL Server Native Client OLE DB provider, data source objects
- OLE DB data source objects [SQL Server Native Client]
- data source objects [OLE DB]
- CLSID
ms.assetid: c1d4ed20-ad3b-4e33-a26b-38d7517237b7
caps.latest.revision: "33"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7f20bf4aee0befa6fb3439da84eef1a04e8ac04a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="data-source-objects-ole-db"></a>데이터 원본 개체(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client와 같은 데이터 저장소에 대 한 링크를 설정 하는 데 사용 되는 OLE DB 인터페이스 집합에 대 한 데이터 원본 이라는 용어를 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 첫 번째 작업은 공급자의 데이터 원본 개체의 인스턴스를 만들지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 소비자입니다.  
  
 각 OLE DB 공급자는 자체적으로 사용할 CLSID(클래스 식별자)를 선언합니다. 에 대 한 CLSID는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 C/c + + GUID CLSID_SQLNCLI10 (SQLNCLI_CLSID 올바른로 확인 되는 기호 참조 하는 sqlncli.h 파일에 progid). CLSID를 소비자에서 사용 하 여 OLE **CoCreateInstance** 함수를 데이터 원본 개체의 인스턴스를 제조 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client는 in-process 서버입니다. 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 개체를 위해 CLSCTX_INPROC_SERVER 매크로 사용 하 여 실행 컨텍스트를 나타내기 위해 만들어집니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 데이터 원본 개체를 변경할 수 있도록 기존 클러스터에 연결 하는 OLE DB 초기화 인터페이스 노출 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스.  
  
 통해 모든 연결 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자이 옵션을 자동으로 설정 합니다.  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 이 예제에서는 클래스 식별자 매크로 사용 하 여 만듭니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 데이터 원본 개체를 만들고 대 한 참조를 해당 **IDBInitialize** 인터페이스입니다.  
  
```  
IDBInitialize*   pIDBInitialize;  
HRESULT          hr;  
  
hr = CoCreateInstance(CLSID_SQLNCLI10, NULL, CLSCTX_INPROC_SERVER,  
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
  
 성공적으로 만들어지면의 인스턴스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 데이터 원본 개체를 데이터 원본 초기화 하 고 세션을 만들어 여는 소비자 응용 프로그램을 계속할 수 있습니다. OLE DB 세션은 데이터 액세스 및 조작을 가능하게 하는 인터페이스를 제공합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 지정 된 인스턴스에 처음 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 성공적인 데이터 원본 초기화의 일부로 합니다. 연결이 때까지 또는 모든 데이터 원본 초기화 인터페이스에 대 한 참조를 유지 관리 되는 그대로 유지 되는 **idbinitialize:: Uninitialize** 메서드를 호출 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [데이터 원본 속성 &#40; OLE db&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-properties-ole-db.md)  
  
-   [데이터 원본 정보 속성](../../relational-databases/native-client-ole-db-data-source-objects/data-source-information-properties.md)  
  
-   [초기화 및 권한 부여 속성](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)  
  
-   [세션](../../relational-databases/native-client-ole-db-data-source-objects/sessions.md)  
  
-   [세션 속성 - SQL Server Native Client OLE DB 공급자](../../relational-databases/native-client-ole-db-data-source-objects/session-properties-sql-server-native-client-ole-db-provider.md)  
  
-   [지속형 데이터 원본 개체](../../relational-databases/native-client-ole-db-data-source-objects/persisted-data-source-objects.md)  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server Native Client&#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
