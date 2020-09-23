---
title: BLOB 및 OLE 개체(OLE DB 드라이버) | Microsoft Docs
description: OLE DB Driver for SQL Server에서 ISequentialStream 인터페이스를 사용하여 대형 이진 개체로 SQL Server 데이터 형식에 대한 소비자 액세스를 지원하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 05/25/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- OLE DB Driver for SQL Server, BLOBs
- large data, OLE objects
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 50c19527b536da0a61d8aa6c7c76ec34010ea268
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861416"
---
# <a name="blobs-and-ole-objects"></a>BLOB 및 OLE 개체
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server는 소비자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **ntext**, **text**<a href="#text_note"><sup>**1**</sup></a>, **image**, **varchar(max)** , **nvarchar(max)** , **varbinary(max)** 및 XML 데이터 형식을 BLOB(Binary Large Object)으로 액세스할 수 있도록 지원하기 위해 **ISequentialStream** 인터페이스를 노출합니다. **ISequentialStream**에서 **Read** 메서드를 사용하면 소비자가 많은 양의 데이터를 관리하기 쉬운 청크로 가져올 수 있습니다.

 <b id="text_note">[1]:</b> UTF-8로 인코딩된 데이터를 레거시 텍스트 열에 삽입하기 위해 ISequentialStream 인터페이스를 사용하는 것은 UTF-8을 지원하는 서버로만 제한됩니다. UTF-8을 지원하지 않는 서버를 대상으로 하는 경우 이 시나리오를 실행하려고 하면 드라이버에서 다음과 같은 오류 메시지를 게시합니다. "선택한 열 유형에 대해 스트리밍이 지원되지 않습니다."

 이 기능을 보여주는 샘플을 보려면 [큰 데이터 설정&#40;OLE DB&#41;](../../oledb/ole-db-how-to/set-large-data-ole-db.md)을 참조하세요.  
  
 소비자가 데이터 수정을 위해 바인딩한 접근자에서 인터페이스 포인터를 제공하면 SQL Server용 OLE DB 드라이버는 소비자가 구현한 **IStorage** 인터페이스를 사용할 수 있습니다.  
  
 큰 값 데이터 형식의 경우 SQL Server용 OLE DB 드라이버는 **IRowset** 및 DDL 인터페이스의 형식 크기 가정을 확인합니다. 최대 크기가 무제한으로 설정된 **varchar**, **nvarchar** 및 **varbinary** 데이터 형식의 열은 열 데이터 형식을 반환하는 스키마 행 집합 및 인터페이스를 통해 ISLONG으로 나타납니다.  
  
 SQL Server용 OLE DB 드라이버는 **varchar(max)** , **varbinary(max)** 및 **nvarchar(max)** 형식을 각각 DBTYPE_STR, DBTYPE_BYTES 및 DBTYPE_WSTR로 노출합니다.  
  
 이러한 형식으로 작업하기 위해 애플리케이션에는 다음 옵션이 있습니다.  
  
-   DBTYPE_STR, DBTYPE_BYTES, DBTYPE_WSTR 형식으로 바인딩합니다. 버퍼 크기가 충분하지 않으면 이전 릴리스에서 이러한 형식을 처리할 때와 마찬가지로 잘림이 발생합니다(새로운 버전에서는 더 큰 값을 사용할 수 있음).  
  
-   형식으로 바인딩하고 DBTYPE_BYREF도 지정합니다.  
  
-   DBTYPE_IUNKNOWN으로 바인딩하고 스트리밍을 사용합니다.  
  
 DBTYPE_IUNKNOWN으로 바인딩하면 ISequentialStream 스트림 기능이 사용됩니다. OLE DB Driver for SQL Server는 큰 값 데이터 형식에 대한 DBTYPE_IUNKNOWN으로 출력 매개 변수를 지원합니다. 이는 저장 프로시저가 이러한 데이터 형식을 반환 값으로 반환하는 시나리오를 지원하기 위한 것이며, 그 값은 클라이언트에 DBTYPE_IUNKNOWN으로 반환됩니다.  
  
## <a name="storage-object-limitations"></a>스토리지 개체 제한 사항  
  
-   OLE DB Driver for SQL Server는 열린 스토리지 개체를 하나만 지원할 수 있습니다. 스토리지 개체를 하나를 초과해 열려고 하면, 즉 하나를 초과하는 **ISequentialStream** 인터페이스 포인터에 대한 참조를 얻으려고 하면 DBSTATUS_E_CANTCREATE가 반환됩니다.  
  
-   SQL Server용 OLE DB 드라이버에서 DBPROP_BLOCKINGSTORAGEOBJECTS 읽기 전용 속성의 기본값은 VARIANT_TRUE입니다. 따라서 스토리지 개체가 활성화되면 스토리지 개체에 있는 메서드를 제외한 일부 메서드가 E_UNEXPECTED 오류와 함께 실패하게 됩니다.  
  
-   소비자가 구현한 스토리지 개체에서 제공하는 데이터의 길이는 이 스토리지 개체를 참조하는 행 접근자가 생성될 때 SQL Server용 OLE DB 드라이버에 알려져 있어야 합니다. 소비자는 접근자 생성에 사용되는 DBBINDING 구조에 길이 표시자를 바인딩해야 합니다.  
  
-   행에 하나를 초과하는 큰 데이터 값이 있고 DBPROP_ACCESSORDER가 DBPROPVAL_AO_RANDOM이 아닌 경우 소비자는 SQL Server용 OLE DB 드라이버 커서 지원 행 집합을 사용하여 행 데이터를 검색하거나 다른 행 값을 검색하기 전에 모든 큰 데이터 값을 처리해야 합니다. DBPROP_ACCESSORDER가 DBPROPVAL_AO_RANDOM인 경우 SQL Server용 OLE DB 드라이버는 임의의 순서로 액세스할 수 있도록 모든 XML 데이터 형식을 BLOB(Binary Large Object)으로 캐시합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [대규모 데이터 가져오기](../../oledb/ole-db-blobs/getting-large-data.md)  
  
-   [대규모 데이터 설정](../../oledb/ole-db-blobs/setting-large-data.md)  
  
-   [BLOB 출력 매개 변수에 대한 스트리밍 지원](../../oledb/ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 프로그래밍용 OLE DB 드라이버](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)        
 [큰 값 형식 사용](../../oledb/features/using-large-value-types.md)  
  
  
