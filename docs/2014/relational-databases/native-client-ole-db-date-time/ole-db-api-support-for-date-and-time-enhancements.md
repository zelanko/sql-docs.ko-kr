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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ba55a2a8fe0ad873c4b5433a53972c441b535333
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704995"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>날짜 및 시간 기능 향상을 위한 OLE DB API 지원
  다음 OLE DB API는 향상된 날짜/시간 기능을 지원합니다.  
  
|기능|설명|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|애플리케이션에서 `datetime`, `datetime2` 및 `smalldatetime` 값을 구분할 수 있도록 DBBINDING 구조체에 플래그가 추가됩니다. 자세한 내용은 [매개 변수 및 행 집합 메타데이터](metadata-parameter-and-rowset.md)를 참조하세요.|  
|IBCPSession::BCPColFmt|자세한 내용은 [향상 된 날짜 및 시간 형식에 대 한 대량 복사 변경 내용 &#40;OLE DB 및 ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)를 참조 하세요.|  
|ICommandWithParameters::GetParameterInfo|자세한 내용은 [매개 변수 및 행 집합 메타데이터](metadata-parameter-and-rowset.md)를 참조하세요.|  
|ICommandWithParameters::SetParameterinfo|자세한 내용은 [매개 변수 및 행 집합 메타데이터](metadata-parameter-and-rowset.md)를 참조하세요.|  
|IColumnsRowset::GetColumnsRowset|자세한 내용은 [매개 변수 및 행 집합 메타데이터](metadata-parameter-and-rowset.md)를 참조하세요.|  
|IColumnsInfo::GetColumnInfo|자세한 내용은 [매개 변수 및 행 집합 메타데이터](metadata-parameter-and-rowset.md)를 참조하세요.|  
|IDBSchemaRowset::GetRowset|영향을 받는 스키마 행 집합에 대한 자세한 내용은 [날짜 및 시간과 스키마 행 집합](../native-client-ole-db-rowsets/rowsets.md)을 참조하세요.|  
|IRowsetFastLoad|이 인터페이스는 새 날짜/시간 형식을 지원하지만 인터페이스 변경 사항은 없습니다.|  
|ITableDefinition::CreateTable|자세한 내용은 [OLE DB 날짜 및 시간 기능 향상을 위한 데이터 형식 지원](data-type-support-for-ole-db-date-and-time-improvements.md)을 참조하세요.|  
  
## <a name="see-also"></a>참고 항목  
 [날짜 및 시간 기능 향상&#40;OLE DB&#41;](date-and-time-improvements-ole-db.md)  
  
  
