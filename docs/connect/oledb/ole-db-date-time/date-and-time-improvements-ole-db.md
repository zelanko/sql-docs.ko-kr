---
title: 날짜 및 시간 기능 향상 (OLE DB) | Microsoft Docs
description: 날짜 및 시간 기능 향상 (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 56a6458e7923e1ae2365e09ae382179981470ab8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="date-and-time-improvements-ole-db"></a>날짜 및 시간 기능 향상 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]에는 새로운 날짜 및 시간 데이터 형식이 도입되었습니다. 이 섹션에서는 SQL Server 용 OLE DB 드라이버에서 확장으로 이러한 새로운 형식이 노출 되는 방법에 대해 설명 합니다. OLE DB 드라이버는 새 날짜 및 시간 데이터 형식에 대 한 SQL Server 지원에 대 한 개요를 참조 하십시오. [날짜 및 시간 기능 향상](../../oledb/features/date-and-time-improvements.md)합니다. 샘플을 보려면 [사용 하 여 향상 된 날짜 및 시간 기능 &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md)합니다.  
  
 날짜 및 시간 데이터 형식에 대 한 자세한 내용은 참조 하십시오. [datetime &#40;TRANSACT-SQL&#41;](../../../t-sql/data-types/datetime-transact-sql.md)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [OLE DB 날짜 및 시간 기능 향상을 위한 데이터 형식 지원](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 OLE DB (OLE DB Driver for SQL Server)에 대 한 정보를 지 원하는 형식을 제공 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 날짜 및 시간 데이터 형식입니다.  
  
 [메타 데이터 &#40;OLE DB&#41;](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)  
 DBBINDING 구조에 대 한 정보를 포함 **icommandwithparameters:: Getparameterinfo**, **icommandwithparameters:: Setparameterinfo**, **IColumnsRowset:: GetColumnsRowset**, 장치 및**ColumnsInfo::GetColumnInfo**합니다. OLE DB 스키마 행 집합의 업데이트에 대한 정보도 제공합니다.  
  
 [바인딩 및 변환 &#40;OLE DB&#41;](../../oledb/ole-db-date-time/conversions-ole-db.md)  
 기존 데이터 형식 및 새로운 데이터 형식에 대한 서버와 클라이언트 간 변환 규칙을 설명합니다.  
  
 [대량 복사 변경 사항으로 향상 된 날짜 및 시간 형식에 대 한 &#40;OLE DB&#41;](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md)  
 대량 복사 작업을 지원하는 날짜/시간 기능 향상에 대해 설명합니다.  
  
 [날짜 및 시간 기능 향상을 위한 OLE DB API 지원](../../oledb/ole-db-date-time/ole-db-api-support-for-date-and-time-enhancements.md)  
 향상된 날짜/시간 기능을 지원하는 OLE DB API에 대해 설명합니다.  
  
 [IRowsetFind 비교](../../oledb/ole-db-date-time/comparability-for-irowsetfind.md)  
 날짜/시간 유형에 대해 설명 하 고 **IRowsetFind**합니다.  
 
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 프로그래밍용 OLE DB 드라이버](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
