---
title: 날짜 및 시간 기능 향상을 위한 OLE DB API 지원 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, date/time improvements
ms.assetid: e65c9253-bd99-4dc3-9cb8-7613f754c966
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ef6334f6fe4671f2563add857f6dd58ce67a2840
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52775825"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>날짜 및 시간 기능 향상을 위한 OLE DB API 지원
  다음 OLE DB API는 향상된 날짜/시간 기능을 지원합니다.  
  
|기능|Description|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|응용 프로그램에서 `datetime`, `datetime2` 및 `smalldatetime` 값을 구분할 수 있도록 DBBINDING 구조체에 플래그가 추가됩니다. 자세한 내용은 [매개 변수 및 행 집합 메타 데이터](metadata-parameter-and-rowset.md)입니다.|  
|IBCPSession::BCPColFmt|자세한 내용은 [향상 된 날짜 및 시간 형식에 대 한 대량 복사 변경 사항 &#40;OLE DB 및 ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)합니다.|  
|ICommandWithParameters::GetParameterInfo|자세한 내용은[매개 변수 및 행 집합 메타 데이터](metadata-parameter-and-rowset.md)입니다.|  
|ICommandWithParameters::SetParameterinfo|자세한 내용은[매개 변수 및 행 집합 메타 데이터](metadata-parameter-and-rowset.md)입니다.|  
|IColumnsRowset::GetColumnsRowset|자세한 내용은[매개 변수 및 행 집합 메타 데이터](metadata-parameter-and-rowset.md)입니다.|  
|IColumnsInfo::GetColumnInfo|자세한 내용은[매개 변수 및 행 집합 메타 데이터](metadata-parameter-and-rowset.md)입니다.|  
|IDBSchemaRowset::GetRowset|영향을 받는 스키마 행 집합의 세부 정보를 참조 하세요[날짜 및 시간과 스키마 행 집합](../native-client-ole-db-rowsets/rowsets.md)합니다.|  
|IRowsetFastLoad|이 인터페이스는 새 날짜/시간 형식을 지원하지만 인터페이스 변경 사항은 없습니다.|  
|ITableDefinition::CreateTable|자세한 내용은 [OLE DB 날짜 및 시간 기능 향상을 위한 데이터 형식 지원](data-type-support-for-ole-db-date-and-time-improvements.md)합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [날짜 및 시간 기능 향상&#40;OLE DB&#41;](date-and-time-improvements-ole-db.md)  
  
  
