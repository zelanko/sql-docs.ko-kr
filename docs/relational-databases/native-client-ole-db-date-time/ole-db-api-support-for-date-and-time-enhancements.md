---
description: 날짜 및 시간 기능 향상을 위한 OLE DB API 지원 (Native Client OLE DB 공급자)
title: 날짜 및 시간 기능 향상을 위한 API 지원 (Native Client OLE DB 공급자)
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: e65c9253-bd99-4dc3-9cb8-7613f754c966
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 753bc7c2ad83d85977729ab7be241fcf4601d4a6
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97433908"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements-native-client-ole-db-provider"></a>날짜 및 시간 기능 향상을 위한 OLE DB API 지원 (Native Client OLE DB 공급자)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  다음 OLE DB API는 향상된 날짜/시간 기능을 지원합니다.  
  
|함수|Description|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|애플리케이션에서 **datetime**, **datetime2** 및 **smalldatetime** 값을 구분할 수 있도록 DBBINDING 구조체에 플래그가 추가됩니다. 자세한 내용은 [매개 변수 및 행 집합 메타데이터](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)를 참조하세요.|  
|IBCPSession::BCPColFmt|자세한 내용은 [향상 된 날짜 및 시간 형식에 대 한 대량 복사 변경 내용 &#40;OLE DB 및 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)를 참조 하세요.|  
|ICommandWithParameters::GetParameterInfo|자세한 내용은 [매개 변수 및 행 집합 메타데이터](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)를 참조하세요.|  
|ICommandWithParameters::SetParameterinfo|자세한 내용은 [매개 변수 및 행 집합 메타데이터](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)를 참조하세요.|  
|IColumnsRowset::GetColumnsRowset|자세한 내용은 [매개 변수 및 행 집합 메타데이터](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)를 참조하세요.|  
|IColumnsInfo::GetColumnInfo|자세한 내용은 [매개 변수 및 행 집합 메타데이터](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)를 참조하세요.|  
|IDBSchemaRowset::GetRowset|영향을 받는 스키마 행 집합에 대한 자세한 내용은 [날짜 및 시간과 스키마 행 집합](../../relational-databases/native-client-ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md)을 참조하세요.|  
|IRowsetFastLoad|이 인터페이스는 새 날짜/시간 형식을 지원하지만 인터페이스 변경 사항은 없습니다.|  
|ITableDefinition::CreateTable|자세한 내용은 [OLE DB 날짜 및 시간 기능 향상을 위한 데이터 형식 지원](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)을 참조하세요.|  
  
## <a name="see-also"></a>참고 항목  
 [날짜 및 시간 기능 향상&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
