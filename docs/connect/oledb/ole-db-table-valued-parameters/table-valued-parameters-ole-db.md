---
title: 테이블 반환 매개 변수 (OLE DB) | Microsoft Docs
description: 테이블 반환 매개 변수(OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, table-valued parameters
- table-valued parameters (OLE DB)
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 13fac7bcfec6dd4470e518429a8f8208e35c4d6e
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43033962"
---
# <a name="table-valued-parameters-ole-db"></a>테이블 반환 매개 변수(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  이 섹션에는 SQL Server에 대 한 OLE DB 드라이버에서 테이블 반환 매개 변수에 대 한 지원을 설명합니다. 추가 개요 정보를 참조 하세요 [테이블 반환 매개 변수 &#40;OLE DB Driver for SQL Server&#41;](../../oledb/features/table-valued-parameters-oledb-driver-for-sql-server.md)합니다. 샘플을 보려면 [테이블 반환 매개 변수 &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)합니다.  
  
## <a name="remarks"></a>Remarks  
 현재 매개 변수 집합(**ICommand::Execute**의 DBPARAMS 매개 변수)을 사용하여 다중 행 데이터를 프로시저에 대한 매개 변수로 서버에 보낼 수 있습니다. 매개 변수 집합을 사용할 경우 해당 집합의 모든 요소가 서버에 개별 RPC(원격 프로시저 호출) 요청으로 서버에 전송되어야 합니다. 테이블 반환 매개 변수는 유사한 기능을 제공하지만 서버와 더 밀접하게 통합됩니다. 따라서 RPC 요청 수가 감소하며 서버에서 집합 기반 작업을 사용할 수 있습니다.  
  
 테이블 반환 매개 변수는 OLE DB로 SQL Server 용 OLE DB 드라이버에서 지원 됩니다 **행 집합** 개체입니다. 소비자(즉, SQL Server용 OLE DB 드라이버를 사용하는 클라이언트 응용 프로그램)는 모든 **Rowset** 개체를 테이블 반환 매개 변수의 자리 표시자로 제공할 수 있습니다. 테이블 반환 매개 변수는 다른 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 매개 변수 유형과 마찬가지로 처리됩니다. OLE DB Driver for SQL Server 만들기, 검색, 사양, 바인딩 및 스키마 인터페이스를 제공합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [테이블 반환 매개 변수 행 집합 만들기](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md)  
  
-   [테이블 반환 매개 변수 형식 검색](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-type-discovery.md)  
  
-   [테이블 반환 매개 변수가 포함된 명령 실행](../../oledb/ole-db-table-valued-parameters/executing-commands-containing-table-valued-parameters.md)  
  
-   [테이블 반환 매개 변수에 데이터 삽입](../../oledb/ole-db-table-valued-parameters/inserting-data-into-table-valued-parameters.md)  
  
-   [OLE DB 테이블 반환 매개 변수에 대해 변경된 스키마 행 집합](../../oledb/ole-db-table-valued-parameters/schema-rowsets-changed-for-ole-db-table-valued-parameters.md)  
  
-   [OLE DB 테이블 반환 매개 변수 형식 지원](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)  
  
-   [OLE DB 테이블 반환 매개 변수 형식 지원&#40;Methods&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md)  
  
-   [OLE DB 테이블 반환 매개 변수 형식 지원&#40;Properties&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 프로그래밍용 OLE DB 드라이버](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)   
 [테이블 반환 매개 변수&#40;OLE DB&#41; 사용](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
