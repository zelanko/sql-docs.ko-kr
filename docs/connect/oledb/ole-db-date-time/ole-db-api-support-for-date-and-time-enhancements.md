---
title: 날짜 및 시간 기능 향상을 위한 API 지원(OLE DB 드라이버)
description: 함수 이름 및 설명을 포함하여 향상된 날짜/시간 기능을 지원하는 OLE DB API에 대해 알아봅니다.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8209c1b1ca6f3c00ce4cd10455c35c8b9d4dfad4
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862357"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>날짜 및 시간 기능 향상을 위한 OLE DB API 지원
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  다음 OLE DB API는 향상된 날짜/시간 기능을 지원합니다.  
  
|함수|Description|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|애플리케이션에서 **datetime**, **datetime2** 및 **smalldatetime** 값을 구분할 수 있도록 DBBINDING 구조체에 플래그가 추가됩니다. 자세한 내용은 [매개 변수 및 행 집합 메타데이터](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)를 참조하세요.|  
|IBCPSession::BCPColFmt|자세한 내용은 [향상된 날짜 및 시간 형식에 대한 대량 복사 변경 사항&#40;OLE DB&#41;](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md)을 참조하세요.|  
|ICommandWithParameters::GetParameterInfo|자세한 내용은 [매개 변수 및 행 집합 메타데이터](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)를 참조하세요.|  
|ICommandWithParameters::SetParameterinfo|자세한 내용은 [매개 변수 및 행 집합 메타데이터](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)를 참조하세요.|  
|IColumnsRowset::GetColumnsRowset|자세한 내용은 [매개 변수 및 행 집합 메타데이터](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)를 참조하세요.|  
|IColumnsInfo::GetColumnInfo|자세한 내용은 [매개 변수 및 행 집합 메타데이터](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)를 참조하세요.|  
|IDBSchemaRowset::GetRowset|영향을 받는 스키마 행 집합에 대한 자세한 내용은 [날짜 및 시간과 스키마 행 집합](../../oledb/ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md)을 참조하세요.|  
|IRowsetFastLoad|이 인터페이스는 새 날짜/시간 형식을 지원하지만 인터페이스 변경 사항은 없습니다.|  
|ITableDefinition::CreateTable|자세한 내용은 [OLE DB 날짜 및 시간 기능 향상을 위한 데이터 형식 지원](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)을 참조하세요.|  
  
## <a name="see-also"></a>참고 항목  
 [날짜 및 시간 기능 향상&#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
