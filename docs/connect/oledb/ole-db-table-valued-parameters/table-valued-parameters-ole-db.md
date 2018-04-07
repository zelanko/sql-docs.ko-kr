---
title: 테이블 반환 매개 변수 (OLE DB) | Microsoft Docs
description: 테이블 반환 매개 변수(OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, table-valued parameters
- table-valued parameters (OLE DB)
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b4c96da8cea62a3357e1b0f50db7cb07341d2a56
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="table-valued-parameters-ole-db"></a>테이블 반환 매개 변수(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  이 섹션에는 SQL Server 용 OLE DB 드라이버에서 테이블 반환 매개 변수에 대 한 지원을 설명합니다. 추가 개요 정보를 참조 하십시오. [테이블 반환 매개 변수 &#40;OLE DB Driver for SQL Server&#41;](../../oledb/features/table-valued-parameters-oledb-driver-for-sql-server.md)합니다. 샘플을 보려면 [테이블 반환 매개 변수 &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)합니다.  
  
## <a name="remarks"></a>주의  
 매개 변수 집합을 사용 하 여 프로시저에 매개 변수로 서버에 여러 행 데이터를 보낼 수는 현재 (의 DBPARAMS 매개 변수 **icommand:: Execute**). 매개 변수 집합을 사용할 경우 해당 집합의 모든 요소가 서버에 개별 RPC(원격 프로시저 호출) 요청으로 서버에 전송되어야 합니다. 테이블 반환 매개 변수는 유사한 기능을 제공하지만 서버와 더 밀접하게 통합됩니다. RPC 요청 수가 줄어들고는 서버에서 집합 기반 작업을 사용 하도록 설정 합니다.  
  
 테이블 반환 매개 변수는 OLE DB로 SQL Server 용 OLE DB 드라이버에서 지원 **행 집합** 개체입니다. 모든 **행 집합** 개체 제공 될 수는 소비자 (즉, 클라이언트 응용 프로그램 OLE DB 드라이버를 사용 하 여 SQL Server 용)가 자리 표시자로 매개 변수 테이블 반환 매개 변수에 대 한 합니다. 테이블 반환 매개 변수는 다른 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 매개 변수 유형과 마찬가지로 처리됩니다. OLE DB Driver for SQL Server 만들기, 검색, 사양, 바인딩 및 스키마 인터페이스를 제공합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [테이블 반환 매개 변수 행 집합 만들기](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md)  
  
-   [테이블 반환 매개 변수 형식 검색](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-type-discovery.md)  
  
-   [테이블 반환 매개 변수가 포함된 명령 실행](../../oledb/ole-db-table-valued-parameters/executing-commands-containing-table-valued-parameters.md)  
  
-   [테이블 반환 매개 변수에 데이터 삽입](../../oledb/ole-db-table-valued-parameters/inserting-data-into-table-valued-parameters.md)  
  
-   [OLE DB 테이블 반환 매개 변수에 대해 변경된 스키마 행 집합](../../oledb/ole-db-table-valued-parameters/schema-rowsets-changed-for-ole-db-table-valued-parameters.md)  
  
-   [OLE DB 테이블 반환 매개 변수 형식 지원](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)  
  
-   [OLE DB 테이블 반환 매개 변수 형식 지원 &#40;메서드&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md)  
  
-   [OLE DB 테이블 반환 매개 변수 형식 지원 &#40;속성&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md)  
  
## <a name="see-also"></a>관련 항목:  
 [OLE DB Driver for SQL Server &#40;OLE DB&#41;](../../oledb/ole-db/oledb-driver-for-sql-server-ole-db.md)   
 [테이블 반환 매개 변수 사용 & #40; OLE db& #41;를 사용 하 여](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
