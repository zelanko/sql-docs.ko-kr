---
title: 날짜 및 시간 기능 향상을 위한 OLE DB API 지원 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: e65c9253-bd99-4dc3-9cb8-7613f754c966
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3c8a474665e65588b2aead4aa6f21394ec76770c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47656471"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>날짜 및 시간 기능 향상을 위한 OLE DB API 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  다음 OLE DB API는 향상된 날짜/시간 기능을 지원합니다.  
  
|기능|Description|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|플래그를 구별 하는 응용 프로그램을 사용 하도록 설정 하려면 DBBINDING 구조에 추가 됩니다 **날짜/시간**를 **datetime2**, 및 **smalldatetime** 값입니다. 자세한 내용은 [매개 변수 및 행 집합 메타 데이터](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)입니다.|  
|IBCPSession::BCPColFmt|자세한 내용은 [향상 된 날짜 및 시간 형식에 대 한 대량 복사 변경 사항 &#40;OLE DB 및 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)합니다.|  
|ICommandWithParameters::GetParameterInfo|자세한 내용은[매개 변수 및 행 집합 메타 데이터](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)입니다.|  
|ICommandWithParameters::SetParameterinfo|자세한 내용은[매개 변수 및 행 집합 메타 데이터](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)입니다.|  
|IColumnsRowset::GetColumnsRowset|자세한 내용은[매개 변수 및 행 집합 메타 데이터](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)입니다.|  
|IColumnsInfo::GetColumnInfo|자세한 내용은[매개 변수 및 행 집합 메타 데이터](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)입니다.|  
|IDBSchemaRowset::GetRowset|영향을 받는 스키마 행 집합의 세부 정보를 참조 하세요[날짜 및 시간과 스키마 행 집합](../../relational-databases/native-client-ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md)합니다.|  
|IRowsetFastLoad|이 인터페이스는 새 날짜/시간 형식을 지원하지만 인터페이스 변경 사항은 없습니다.|  
|ITableDefinition::CreateTable|자세한 내용은 [OLE DB 날짜 및 시간 기능 향상을 위한 데이터 형식 지원](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [날짜 및 시간 기능 향상&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
