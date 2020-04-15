---
title: 데이터 원본 개체(OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d8bb984c789f759eb764ad580f971ab71c9fc946
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297694"
---
# <a name="data-source-objects-ole-db"></a>데이터 원본 개체(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]네이티브 클라이언트는 와 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]데이터 저장소에 대한 링크를 설정하는 데 사용되는 OLE DB 인터페이스 집합에 대해 데이터 원본이라는 용어를 사용합니다. 공급자의 데이터 원본 개체의 인스턴스를 만드는 것은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 소비자의 첫 번째 작업입니다.  
  
 각 OLE DB 공급자는 자체적으로 사용할 CLSID(클래스 식별자)를 선언합니다. 네이티브 클라이언트 OLE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DB 공급자의 CLSID는 C/C++ GUID CLSID_SQLNCLI10(SQLNCLI_CLSID 기호는 참조하는 sqlncli.h 파일에서 올바른 프로기드로 확인됨)입니다. CLSID가 있으면 소비자는 OLE **CoCreateInstance** 함수를 사용하여 데이터 원본 개체의 인스턴스를 만듭니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]네이티브 클라이언트는 프로세스 내 서버입니다. 네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자 개체의 인스턴스는 실행 가능한 컨텍스트를 나타내기 위해 CLSCTX_INPROC_SERVER 매크로를 사용하여 만들어집니다.  
  
 네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자 데이터 원본 개체는 소비자가 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결할 수 있도록 하는 OLE DB 초기화 인터페이스를 노출합니다.  
  
 네이티브 클라이언트 OLE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DB 공급자를 통해 이루어진 모든 연결은 다음 옵션을 자동으로 설정합니다.  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 이 예제에서는 클래스 식별자 매크로를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자 데이터 원본 개체를 만들고 **IDBInitialize** 인터페이스에 대한 참조를 가져옵니다.  
  
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
  
 네이티브 클라이언트 OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공급자 데이터 원본 개체의 인스턴스를 성공적으로 생성하면 소비자 응용 프로그램은 데이터 원본을 초기화하고 세션을 만들어 계속 할 수 있습니다. OLE DB 세션은 데이터 액세스 및 조작을 가능하게 하는 인터페이스를 제공합니다.  
  
 네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자는 성공적인 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원본 초기화의 일부로 지정된 인스턴스에 첫 번째 연결을 만듭니다. 이 연결은 데이터 원본 초기화 인터페이스에 대한 참조가 유지되는 동안이나 **IDBInitialize::Uninitialize** 메서드가 호출될 때까지 유지됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [데이터 원본 속성&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-properties-ole-db.md)  
  
-   [데이터 원본 정보 속성](../../relational-databases/native-client-ole-db-data-source-objects/data-source-information-properties.md)  
  
-   [초기화 및 권한 부여 속성](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)  
  
-   [세션](../../relational-databases/native-client-ole-db-data-source-objects/sessions.md)  
  
-   [세션 속성 - SQL Server Native Client OLE DB 공급자](../../relational-databases/native-client-ole-db-data-source-objects/session-properties-sql-server-native-client-ole-db-provider.md)  
  
-   [지속형 데이터 원본 개체](../../relational-databases/native-client-ole-db-data-source-objects/persisted-data-source-objects.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client&#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
