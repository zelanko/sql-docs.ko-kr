---
title: 날짜 및 시간 기능 향상에 대 한 OLE DB API 지원 | Microsoft Docs
description: 향상 된 날짜 및 시간 기능에 대 한 OLE DB API 지원
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: b3ccbf0a43cd64acb69c084ce75cb3673f38a8f2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>날짜 및 시간 기능 향상에 대 한 OLE DB API 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  다음 OLE DB API는 향상된 날짜/시간 기능을 지원합니다.  
  
|함수|Description|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|응용 프로그램 구분에 사용할 수 있도록 DBBINDING 구조에 플래그가 추가 됩니다 **datetime**, **datetime2**, 및 **smalldatetime** 값입니다. 자세한 내용은 참조 [매개 변수 및 행 집합 메타 데이터](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)합니다.|  
|Ibcpsession:: Bcpcolfmt|자세한 내용은 참조 [향상 된 날짜 및 시간 형식에 대 한 대량 복사 변경 사항 &#40;OLE DB&#41;](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md)합니다.|  
|ICommandWithParameters::GetParameterInfo|자세한 내용은 참조[매개 변수 및 행 집합 메타 데이터](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)합니다.|  
|ICommandWithParameters::SetParameterinfo|자세한 내용은 참조[매개 변수 및 행 집합 메타 데이터](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)합니다.|  
|IColumnsRowset::GetColumnsRowset|자세한 내용은 참조[매개 변수 및 행 집합 메타 데이터](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)합니다.|  
|IColumnsInfo::GetColumnInfo|자세한 내용은 참조[매개 변수 및 행 집합 메타 데이터](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)합니다.|  
|IDBSchemaRowset::GetRowset|영향을 받는 스키마 행 집합의 세부 정보를 참조 하십시오.[날짜 및 시간과 스키마 행 집합](../../oledb/ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md)합니다.|  
|IRowsetFastLoad|이 인터페이스는 새 날짜/시간 형식을 지원하지만 인터페이스 변경 사항은 없습니다.|  
|ITableDefinition::CreateTable|자세한 내용은 참조 [OLE DB 날짜 및 시간 기능 향상에 대 한 데이터 형식 지원](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [날짜 및 시간 기능 향상 & #40; OLE db& #41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
