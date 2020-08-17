---
description: Blob 및 OLE 개체 (Native Client OLE DB 공급자)
title: Blob 및 OLE 개체 (Native Client OLE DB 공급자) | Microsoft Docs
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
ms.openlocfilehash: c9ab95bece59c6ecb2ed3c2df4aeb0b90ec52605
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88381206"
---
# <a name="blobs-and-ole-objects-in-sql-server-native-client"></a>SQL Server Native Client의 Blob 및 OLE 개체
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ISequentialStream** Native Client OLE DB 공급자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ntext**, **text**, **image**, **varchar (max)**, **nvarchar (max**), **varbinary (max)** 및 xml 데이터 형식에 대 한 소비자 액세스를 blob (binary large object)로 지원 하기 위해 ISequentialStream 인터페이스를 노출 합니다. **ISequentialStream**에서 **Read** 메서드를 사용하면 소비자가 많은 양의 데이터를 관리하기 쉬운 청크로 가져올 수 있습니다.  
  
 이 기능을 보여주는 샘플을 보려면 [큰 데이터 설정&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/set-large-data-ole-db.md)을 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]소비자가 데이터 수정에 바인딩된 접근자에 인터페이스 포인터를 제공 하는 경우 Native Client OLE DB 공급자는 소비자가 구현한 **IStorage** 인터페이스를 사용할 수 있습니다.  
  
 큰 값 데이터 형식의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 **IROWSET** 및 DDL 인터페이스에서 형식 크기 가정을 확인 합니다. 최대 크기가 무제한으로 설정 된 **varchar**, **nvarchar**및 **varbinary** 데이터 형식의 열은 스키마 행 집합 및 열 데이터 형식을 반환 하는 인터페이스를 통해 islong으로 표시 됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 varchar ( **max)**, **varbinary (max)** 및 **nvarchar (max)** 형식을 각각 DBTYPE_STR, DBTYPE_BYTES 및 DBTYPE_WSTR으로 노출 합니다.  
  
 애플리케이션에서 이러한 형식을 사용하기 위해 처리하는 방법은 다음과 같습니다.  
  
-   DBTYPE_STR, DBTYPE_BYTES, DBTYPE_WSTR 형식으로 바인딩합니다. 버퍼 크기가 충분하지 않으면 이전 릴리스에서 이러한 형식을 처리할 때와 마찬가지로 잘림이 발생합니다(새로운 버전에서는 더 큰 값을 사용할 수 있음).  
  
-   형식으로 바인딩하고 DBTYPE_BYREF도 지정합니다.  
  
-   DBTYPE_IUNKNOWN으로 바인딩하고 스트리밍을 사용합니다.  
  
 DBTYPE_IUNKNOWN으로 바인딩하면 ISequentialStream 스트림 기능이 사용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native client OLE DB 공급자는 출력 매개 변수를 대량 값 데이터 형식에 대 한 DBTYPE_IUNKNOWN로 바인딩하는 데 사용할 수 있습니다 .이 경우 저장 프로시저는 이러한 데이터 형식을 클라이언트에 DBTYPE_IUNKNOWN으로 노출 되는 반환 값으로 반환 합니다.  
  
## <a name="storage-object-limitations"></a>스토리지 개체 제한 사항  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 열려 있는 단일 저장소 개체만 지원할 수 있습니다. 스토리지 개체를 하나를 초과해 열려고 하면, 즉 하나를 초과하는 **ISequentialStream** 인터페이스 포인터에 대한 참조를 얻으려고 하면 DBSTATUS_E_CANTCREATE가 반환됩니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자에서 DBPROP_BLOCKINGSTORAGEOBJECTS 읽기 전용 속성의 기본값은 VARIANT_TRUE입니다. 이는 스토리지 개체가 활성화되면 스토리지 개체에 있는 메서드를 제외한 일부 메서드가 E_UNEXPECTED 오류와 함께 실패한다는 것을 의미합니다.  
  
-   소비자가 구현한 저장소 개체에서 제공 하는 데이터의 길이는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장소 개체를 참조 하는 행 접근자가 만들어질 때 Native Client OLE DB 공급자에 게 알려 두어야 합니다. 소비자는 접근자 생성에 사용되는 DBBINDING 구조에 길이 표시자를 바인딩해야 합니다.  
  
-   한 행에 두 개 이상의 대량 데이터 값이 포함 되어 DBPROP_ACCESSORDER DBPROPVAL_AO_RANDOM 되지 않은 경우 소비자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 커서 지원 행 집합을 사용 하 여 행 데이터를 검색 하거나 다른 행 값을 검색 하기 전에 모든 대량 데이터 값을 처리 해야 합니다. DBPROP_ACCESSORDER DBPROPVAL_AO_RANDOM 되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 모든 xml 데이터 형식을 blob (binary large object)로 캐시 하 여 순서에 관계 없이 액세스할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [대규모 데이터 가져오기](../../relational-databases/native-client-ole-db-blobs/getting-large-data.md)  
  
-   [대규모 데이터 설정](../../relational-databases/native-client-ole-db-blobs/setting-large-data.md)  
  
-   [BLOB 출력 매개 변수에 대한 스트리밍 지원](../../relational-databases/native-client-ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [큰 값 형식 사용](../../relational-databases/native-client/features/using-large-value-types.md)  
  
  
