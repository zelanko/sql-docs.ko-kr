---
title: 날짜 및 시간 기능 향상 (OLE DB) | Microsoft Docs
description: 날짜 및 시간 기능 향상(OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
author: pmasl
ms.author: pelopes
ms.openlocfilehash: c4a93078b84cf5146f94043496bea0fdaed9fc80
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015697"
---
# <a name="date-and-time-improvements-ole-db"></a>날짜 및 시간 기능 향상(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]에는 새로운 날짜 및 시간 데이터 형식이 도입되었습니다. 이 섹션에서는 이러한 새 형식이 SQL Server에 대 한 OLE DB 드라이버에서 확장으로 노출 되는 방법에 대해 설명 합니다. 새 날짜 및 시간 데이터 형식에 대 한 SQL Server 지원 OLE DB 드라이버의 개요는 [날짜 및 시간 기능 향상](../../oledb/features/date-and-time-improvements.md)을 참조 하세요. 샘플은 [OLE DB &#40;&#41;향상 된 날짜 및 시간 기능 사용](../../oledb/ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md)을 참조 하세요.  
  
 날짜 및 시간 데이터 형식에 대 한 일반적인 정보는 [datetime &#40;transact-sql&#41;](../../../t-sql/data-types/datetime-transact-sql.md)을 참조 하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [OLE DB 날짜 및 시간 기능 향상을 위한 데이터 형식 지원](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 날짜 및 시간 데이터 형식을 지 원하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB (SQL Server 용 OLE DB 드라이버) 유형에 대 한 정보를 제공 합니다.  
  
 [메타 &#40;데이터 OLE DB&#41;](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)  
 DBBINDING 구조, **ICommandWithParameters:: GetParameterInfo**, **ICommandWithParameters:: SetParameterInfo**, **IColumnsRowset:: GetColumnsRowset**및 I에 대 한 정보를 포함 합니다. **: GetColumnInfo** . OLE DB 스키마 행 집합의 업데이트에 대한 정보도 제공합니다.  
  
 [바인딩 및 변환&#40;OLE DB&#41;](../../oledb/ole-db-date-time/conversions-ole-db.md)  
 기존 데이터 형식 및 새로운 데이터 형식에 대한 서버와 클라이언트 간 변환 규칙을 설명합니다.  
  
 [향상된 날짜 및 시간 형식에 대한 대량 복사 변경 사항&#40;OLE DB&#41;](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md)  
 대량 복사 작업을 지원하는 날짜/시간 기능 향상에 대해 설명합니다.  
  
 [날짜 및 시간 기능 향상을 위한 OLE DB API 지원](../../oledb/ole-db-date-time/ole-db-api-support-for-date-and-time-enhancements.md)  
 향상된 날짜/시간 기능을 지원하는 OLE DB API에 대해 설명합니다.  
  
 [IRowsetFind 비교](../../oledb/ole-db-date-time/comparability-for-irowsetfind.md)  
 날짜/시간 형식 및 **IRowsetFind**에 대해 설명 합니다.  
 
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 프로그래밍용 OLE DB 드라이버](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
