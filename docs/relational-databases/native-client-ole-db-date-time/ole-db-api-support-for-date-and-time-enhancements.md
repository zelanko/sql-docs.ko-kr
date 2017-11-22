---
title: "날짜 및 시간 기능 향상에 대 한 OLE DB API 지원 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-date-time
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: e65c9253-bd99-4dc3-9cb8-7613f754c966
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4f33b6aa10205aa13203384a39201642f94c5a4b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>날짜 및 시간 기능 향상에 대 한 OLE DB API 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  다음 OLE DB API는 향상된 날짜/시간 기능을 지원합니다.  
  
|함수|Description|  
|--------------|-----------------|  
|Iaccessor:: Createaccessor|응용 프로그램 구분에 사용할 수 있도록 DBBINDING 구조에 플래그가 추가 됩니다 **datetime**, **datetime2**, 및 **smalldatetime** 값입니다. 자세한 내용은 참조 [매개 변수 및 행 집합 메타 데이터](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)합니다.|  
|Ibcpsession:: Bcpcolfmt|자세한 내용은 참조 [향상 된 날짜 및 시간 형식 &#40; OLE DB 및 ODBC &#41;에 대 한 대량 복사 변경 사항](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)합니다.|  
|ICommandWithParameters::GetParameterInfo|자세한 내용은 참조[매개 변수 및 행 집합 메타 데이터](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)합니다.|  
|Icommandwithparameters::|자세한 내용은 참조[매개 변수 및 행 집합 메타 데이터](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)합니다.|  
|IColumnsRowset::GetColumnsRowset|자세한 내용은 참조[매개 변수 및 행 집합 메타 데이터](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)합니다.|  
|IColumnsInfo::GetColumnInfo|자세한 내용은 참조[매개 변수 및 행 집합 메타 데이터](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md)합니다.|  
|Idbschemarowset:: Getrowset|영향을 받는 스키마 행 집합의 세부 정보를 참조 하십시오.[날짜 및 시간과 스키마 행 집합](../../relational-databases/native-client-ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md)합니다.|  
|IRowsetFastLoad|이 인터페이스는 새 날짜/시간 형식을 지원하지만 인터페이스 변경 사항은 없습니다.|  
|Itabledefinition:: Createtable|자세한 내용은 참조 [OLE DB 날짜 및 시간 기능 향상에 대 한 데이터 형식 지원](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [날짜 및 시간 기능 향상 &#40; OLE db&#41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
