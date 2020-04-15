---
title: BLOB 및 OLE 개체 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- SQL Server Native Client OLE DB provider, BLOBs
- large data, OLE objects
ms.assetid: 767fa2f6-9cd2-436f-add5-e760bed29a58
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d0cb9751940489513f939ab8ee52728c6b75e925
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297697"
---
# <a name="blobs-and-ole-objects"></a>BLOB 및 OLE 개체
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자는 **ntext,** **텍스트,** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **이미지,** **varchar(최대)** 및 **varvarchar(최대)** 및 **xml**데이터 형식에 대한 소비자 액세스를 지원하기 위해 **I사적 Stream** 인터페이스를 이진 큰 개체(BLOB)로 노출합니다. **ISequentialStream**에서 **Read** 메서드를 사용하면 소비자가 많은 양의 데이터를 관리하기 쉬운 청크로 가져올 수 있습니다.  
  
 이 기능을 보여주는 샘플을 보려면 [큰 데이터 설정&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/set-large-data-ole-db.md)을 참조하세요.  
  
 네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자는 소비자가 데이터 수정을 위해 바인딩된 접근자에서 인터페이스 포인터를 제공하는 경우 소비자 구현 **IStorage** 인터페이스를 사용할 수 있습니다.  
  
 큰 값 데이터 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 경우 네이티브 클라이언트 OLE DB 공급자는 **IRowset** 및 DDL 인터페이스에서 형식 크기 가정을 확인합니다. **varchar,** **nvarchar**및 최대 크기가 무제한으로 설정된 varbinary 데이터 형식이 있는 **열은** 스키마 행 집합 및 반환 열 데이터 형식을 통해 ISLONG으로 표시됩니다.  
  
 네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자는 **varchar(최대)** 및 **varbinary(최대)** 및 **nvarchar(max)** 형식을 각각 DBTYPE_STR, DBTYPE_BYTES 및 DBTYPE_WSTR 노출합니다.  
  
 애플리케이션에서 이러한 형식을 사용하기 위해 처리하는 방법은 다음과 같습니다.  
  
-   DBTYPE_STR, DBTYPE_BYTES, DBTYPE_WSTR 형식으로 바인딩합니다. 버퍼 크기가 충분하지 않으면 이전 릴리스에서 이러한 형식을 처리할 때와 마찬가지로 잘림이 발생합니다(새로운 버전에서는 더 큰 값을 사용할 수 있음).  
  
-   형식으로 바인딩하고 DBTYPE_BYREF도 지정합니다.  
  
-   DBTYPE_IUNKNOWN으로 바인딩하고 스트리밍을 사용합니다.  
  
 DBTYPE_IUNKNOWN으로 바인딩하면 ISequentialStream 스트림 기능이 사용됩니다. 네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자는 큰 값 데이터 형식에 대 한 DBTYPE_IUNKNOWN 바인딩 된 출력 매개 변수를 지원 저장 프로시저가 클라이언트에 DBTYPE_IUNKNOWN 으로 노출 될 반환 값으로 이러한 데이터 형식을 반환 하는 시나리오를 용이 하 게 합니다.  
  
## <a name="storage-object-limitations"></a>스토리지 개체 제한 사항  
  
-   네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자는 열려 있는 단일 저장소 개체만 지원할 수 있습니다. 스토리지 개체를 하나를 초과해 열려고 하면, 즉 하나를 초과하는 **ISequentialStream** 인터페이스 포인터에 대한 참조를 얻으려고 하면 DBSTATUS_E_CANTCREATE가 반환됩니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자에서 DBPROP_BLOCKINGSTORAGEOBJECTS 읽기 전용 속성의 기본값은 VARIANT_TRUE. 이는 스토리지 개체가 활성화되면 스토리지 개체에 있는 메서드를 제외한 일부 메서드가 E_UNEXPECTED 오류와 함께 실패한다는 것을 의미합니다.  
  
-   소비자 구현 저장소 개체가 제공하는 데이터의 길이는 저장소 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체를 참조하는 행 접근자가 생성될 때 네이티브 클라이언트 OLE DB 공급자에게 알려야 합니다. 소비자는 접근자 생성에 사용되는 DBBINDING 구조에 길이 표시자를 바인딩해야 합니다.  
  
-   행에 둘 이상의 큰 데이터 값이 포함되어 있고 DBPROP_ACCESSORDER DBPROPVAL_AO_RANDOM 않은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 경우 소비자는 네이티브 클라이언트 OLE DB 공급자 커서 지원 행 집합을 사용하여 행 데이터를 검색하거나 다른 행 값을 검색하기 전에 모든 큰 데이터 값을 처리해야 합니다. DBPROP_ACCESSORDER DBPROPVAL_AO_RANDOM [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자는 모든 xml 데이터 형식을 이진 대형 개체(BLOB)로 캐시하여 순서에 따라 액세스할 수 있도록 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [대규모 데이터 가져오기](../../relational-databases/native-client-ole-db-blobs/getting-large-data.md)  
  
-   [대규모 데이터 설정](../../relational-databases/native-client-ole-db-blobs/setting-large-data.md)  
  
-   [BLOB 출력 매개 변수에 대한 스트리밍 지원](../../relational-databases/native-client-ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL 서버 네이티브 클라이언트 &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [큰 값 형식 사용](../../relational-databases/native-client/features/using-large-value-types.md)  
  
  
