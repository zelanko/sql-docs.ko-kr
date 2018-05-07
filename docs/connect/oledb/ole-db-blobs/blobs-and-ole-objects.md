---
title: Blob 및 OLE 개체 | Microsoft Docs
description: BLOB 및 OLE 개체
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-blobs
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- OLE DB Driver for SQL Server, BLOBs
- large data, OLE objects
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: e78fe8db35684bb35e4111a38d3d0ba938891785
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="blobs-and-ole-objects"></a>BLOB 및 OLE 개체
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB Driver for SQL Server 노출 된 **ISequentialStream** 소비자에 대 한 액세스를 지원 하기 위해 인터페이스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **ntext**, **텍스트**, **이미지** , **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, 형식과 xml 데이터 형식으로 이진 대형 개체 (Blob). **읽기** 메서드를 **ISequentialStream** 소비자를 관리 하기 쉬운 청크로 많은 데이터를 검색할 수 있습니다.  
  
 이 기능을 보여 주는 샘플을 보려면 [대형 데이터 설정 & #40; OLE DB & #41;](../../oledb/ole-db-how-to/set-large-data-ole-db.md)합니다.  
  
 OLE DB Driver for SQL Server 소비자가 구현한 צ ְ ײ **IStorage** 인터페이스 소비자는 접근자에서 인터페이스 포인터를 제공 하는 경우 데이터 수정을 위해 바인딩한 합니다.  
  
 큰 값 데이터 형식에 대 한는 OLE DB Driver for SQL Server에서 형식 크기 가정을 확인 **IRowset** 및 DDL 인터페이스입니다. 열이 있는 **varchar**, **nvarchar**, 및 **varbinary** 데이터 형식 및 최대 크기가 무제한으로 설정 됩니다 ISLONG으로 나타납니다을 통해 스키마 행 집합 열 데이터 형식을 반환 하는 인터페이스입니다.  
  
 OLE DB Driver for SQL Server 노출 된 **varchar (max)**, **varbinary (max)** 및 **nvarchar (max)** 형식을 각각 DBTYPE_STR, DBTYPE_BYTES 및 DBTYPE_WSTR로 합니다.  
  
 이러한 형식으로 작업하기 위해 응용 프로그램에는 다음 옵션이 있습니다.  
  
-   DBTYPE_STR, DBTYPE_BYTES, DBTYPE_WSTR 형식으로 바인딩합니다. 버퍼가 크면 충분 한 잘림이 발생 합니다, 이전 버전에서는 이러한 종류의 경우와 정확히 (값이 클수록 이제 사용할 수 있지만).  
  
-   형식으로 바인딩하고 DBTYPE_BYREF도 지정합니다.  
  
-   DBTYPE_IUNKNOWN으로 바인딩하고 스트리밍을 사용합니다.  
  
 DBTYPE_IUNKNOWN으로 바인딩하면 ISequentialStream 스트림 기능이 사용됩니다. OLE DB Driver for SQL Server는 큰 값 데이터 형식에 대 한 DBTYPE_IUNKNOWN으로 바인딩 출력 매개 변수를 지원합니다. 이 저장된 프로시저가 클라이언트에 DBTYPE_IUNKNOWN으로 반환 하는 반환 값으로 이러한 데이터 형식은 반환 하는 시나리오를 지 원하는입니다.  
  
## <a name="storage-object-limitations"></a>저장소 개체 제한 사항  
  
-   OLE DB Driver for SQL Server는 열려 있는 저장소 개체를 지원할 수 있습니다. 둘 이상의 저장소 개체를 열면 (하나 이상에 대 한 참조를 가져오려면 **ISequentialStream** 인터페이스 포인터) DBSTATUS_E_CANTCREATE가 반환 됩니다.  
  
-   OLE DB 드라이버에서 SQL Server에 대 한 DBPROP_BLOCKINGSTORAGEOBJECTS 읽기 전용 속성의 기본값이 VARIANT_TRUE입니다. 따라서 저장소 개체가 활성화 되 면 일부 메서드 (이외의 다른 저장소 개체에 있는 메서드의) E_UNEXPECTED로 실패 합니다.  
  
-   소비자가 구현한 저장소 개체에 의해 표시 되는 데이터의 길이 수 있는 알려진 OLE DB Driver for SQL Server 저장소 개체를 참조 하는 행 접근자를 만들 때. 소비자는 접근자 생성에 사용되는 DBBINDING 구조에 길이 표시자를 바인딩해야 합니다.  
  
-   행에 포함 된 둘 이상의 큰 데이터 값 및 DBPROP_ACCESSORDER가 dbpropval_ao_random이 아닌, 소비자 행 데이터를 검색 하거나 다른 검색 하기 전에 모든 큰 데이터 값이 처리 되는 OLE DB Driver for SQL Server 커서 지원 행 집합을 사용 하거나 해야 행 값입니다. DBPROP_ACCESSORDER가 dbpropval_ao_random 인, 어떤 순서로 든 액세스할 수 있도록는 OLE DB Driver for SQL Server 이진 대형 개체 (Blob)으로 모든 xml 데이터 형식은 캐시 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [대규모 데이터 가져오기](../../oledb/ole-db-blobs/getting-large-data.md)  
  
-   [대규모 데이터 설정](../../oledb/ole-db-blobs/setting-large-data.md)  
  
-   [BLOB 출력 매개 변수에 대 한 스트리밍 지원](../../oledb/ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 프로그래밍에 대 한 OLE DB 드라이버](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)        
 [큰 값 형식 사용](../../oledb/features/using-large-value-types.md)  
  
  
