---
title: Blob 및 OLE 개체 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- SQL Server Native Client OLE DB provider, BLOBs
- large data, OLE objects
ms.assetid: 767fa2f6-9cd2-436f-add5-e760bed29a58
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 80629d81a9212801e65e272f5790b0cc57a11103
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37428742"
---
# <a name="blobs-and-ole-objects"></a>BLOB 및 OLE 개체
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 노출 하는 **ISequentialStream** 소비자에 대 한 액세스를 지원 하기 위해 인터페이스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ntext**를 **텍스트**, **이미지**, **varchar (max)** 를 **nvarchar (max)** 하십시오 **varbinary (max)**, 및 xml 데이터 형식을 Blob (binary large object ). 합니다 **읽기** 메서드를 **ISequentialStream** 소비자 관리 가능한 청크로 많은 데이터를 검색할 수 있습니다.  
  
 이 기능을 보여 주는 샘플을 참조 하세요 [큰 데이터 집합 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/set-large-data-ole-db.md)합니다.  
  
 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 소비자가 구현한 따르면 **IStorage** 데이터 수정을 위해 바인딩한 접근자에서 인터페이스 포인터를 제공 하는 소비자 때 인터페이스입니다.  
  
 큰 값 데이터 형식에 대 한 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자의 형식 크기 가정을 확인 **IRowset** 및 DDL 인터페이스입니다. 열 **varchar**를 **nvarchar**, 및 **varbinary** 무제한으로 설정 하는 최대 크기를 사용 하 여 데이터 형식이 스키마 행 집합 및 인터페이스를 통해 ISLONG으로 표현 열 데이터 형식을 반환 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 노출 하는 **varchar (max)**, **varbinary (max)** 하 고 **nvarchar (max)** DBTYPE_STR, DBTYPE_BYTES 및 DBTYPE_ 형식 WSTR 각각.  
  
 응용 프로그램에서 이러한 형식을 사용하기 위해 처리하는 방법은 다음과 같습니다.  
  
-   DBTYPE_STR, DBTYPE_BYTES, DBTYPE_WSTR 형식으로 바인딩합니다. 버퍼 크기가 충분하지 않으면 이전 릴리스에서 이러한 형식을 처리할 때와 마찬가지로 잘림이 발생합니다(새로운 버전에서는 더 큰 값을 사용할 수 있음).  
  
-   형식으로 바인딩하고 DBTYPE_BYREF도 지정합니다.  
  
-   DBTYPE_IUNKNOWN으로 바인딩하고 스트리밍을 사용합니다.  
  
 DBTYPE_IUNKNOWN으로 바인딩하면 ISequentialStream 스트림 기능이 사용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 저장된 프로시저를 이러한 데이터를 반환 하는 시나리오를 용이 하 게 큰 값 데이터 형식에 대해 DBTYPE_IUNKNOWN 형식을 반환 값으로 노출 될 DBTYPE_IUNKNOWN으로 바인딩 출력 매개 변수 지원 클라이언트입니다.  
  
## <a name="storage-object-limitations"></a>저장소 개체 제한 사항  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 열려 있는 저장소 개체를 지원할 수 있습니다. 둘 이상의 저장소 개체를 열려고 시도 (하나 이상에 대 한 참조를 가져오려고 **ISequentialStream** 인터페이스 포인터) DBSTATUS_E_CANTCREATE가 반환 됩니다.  
  
-   에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에서 DBPROP_BLOCKINGSTORAGEOBJECTS 읽기 전용 속성의 기본값은 VARIANT_TRUE입니다. 이는 저장소 개체가 활성화되면 저장소 개체에 있는 메서드를 제외한 일부 메서드가 E_UNEXPECTED 오류와 함께 실패한다는 것을 의미합니다.  
  
-   소비자가 구현한 저장소 개체에 의해 표시 되는 데이터의 길이를 알 수 있어야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 저장소 개체를 참조 하는 행 접근자를 만들 때. 소비자는 접근자 생성에 사용되는 DBBINDING 구조에 길이 표시자를 바인딩해야 합니다.  
  
-   행을 큰 데이터 값 이상 있고 DBPROP_ACCESSORDER가 DBPROPVAL_AO_RANDOM이 아닌 경우 소비자에서 사용 해야 합니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 커서 지원 행 집합 행 데이터를 검색 하거나 모든 큰 데이터를 처리 하기 전에 값 다른 행 값을 검색합니다. DBPROP_ACCESSORDER가 DBPROPVAL_AO_RANDOM 인 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 순서에 관계 없이 액세스할 수 있도록 모든 xml 데이터 형식 binary large object (Blob)으로 캐시 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [대규모 데이터 가져오기](../../relational-databases/native-client-ole-db-blobs/getting-large-data.md)  
  
-   [대규모 데이터 설정](../../relational-databases/native-client-ole-db-blobs/setting-large-data.md)  
  
-   [BLOB 출력 매개 변수에 대한 스트리밍 지원](../../relational-databases/native-client-ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [큰 값 형식 사용](../../relational-databases/native-client/features/using-large-value-types.md)  
  
  
