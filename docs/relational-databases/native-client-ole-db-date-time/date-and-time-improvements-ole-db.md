---
title: 날짜 및 시간 기능 향상 (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
ms.assetid: 71614aaf-0fa4-4fe0-b522-68e2e0b66f43
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dc78f8c63b24b72dbfb09887fbf7db54dc0f4efe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107025"
---
# <a name="date-and-time-improvements-ole-db"></a>날짜 및 시간 기능 향상(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에는 새로운 날짜 및 시간 데이터 형식이 도입되었습니다. 이 섹션에서는 이러한 새로운 형식이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 확장에서 어떤 방식으로 나타나는지 설명합니다. 에 대 한 개요는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 지원 새 날짜 및 시간 데이터 형식에 대 한 참조 [날짜 및 시간 기능 향상](../../relational-databases/native-client/features/date-and-time-improvements.md)합니다. 샘플을 보려면 [사용 하 여 향상 된 날짜 및 시간 기능 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md)합니다.  
  
 날짜 및 시간 데이터 형식에 대 한 자세한 내용을 보려면 [datetime &#40;Transact SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md).  
  
## <a name="in-this-section"></a>섹션 내용  
 [OLE DB 날짜 및 시간 기능 향상을 위한 데이터 형식 지원](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 OLE DB에 대 한 정보를 제공 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client) 지 원하는 형식을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 날짜 및 시간 데이터 형식입니다.  
  
 [메타 데이터 &#40;OLE DB&#41;](https://msdn.microsoft.com/library/605e3be5-aeea-4573-9847-b866ed3c8bff)  
 DBBINDING 구조에 대 한 정보를 포함 **icommandwithparameters:: Getparameterinfo**하십시오 **icommandwithparameters:: Setparameterinfo**, **IColumnsRowset:: GetColumnsRowset**, 및 I**ColumnsInfo::GetColumnInfo**합니다. OLE DB 스키마 행 집합의 업데이트에 대한 정보도 제공합니다.  
  
 [바인딩 및 변환&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/conversions-ole-db.md)  
 기존 데이터 형식 및 새로운 데이터 형식에 대한 서버와 클라이언트 간 변환 규칙을 설명합니다.  
  
 [향상 된 날짜 및 시간 형식에 대 한 복사본의 변경 내용을 대량 &#40;OLE DB 및 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 대량 복사 작업을 지원하는 날짜/시간 기능 향상에 대해 설명합니다.  
  
 [날짜 및 시간 기능 향상을 위한 OLE DB API 지원](../../relational-databases/native-client-ole-db-date-time/ole-db-api-support-for-date-and-time-enhancements.md)  
 향상된 날짜/시간 기능을 지원하는 OLE DB API에 대해 설명합니다.  
  
 [IRowsetFind 비교](../../relational-databases/native-client-ole-db-date-time/comparability-for-irowsetfind.md)  
 날짜/시간 형식에 설명 하 고 **IRowsetFind**합니다.  
  
 [새 날짜 및 시간 기능 이전 버전의 SQL Server 사용 하 여 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/new-date-and-time-features-with-previous-sql-server-versions-ole-db.md)  
 향상된 날짜 및 시간 기능을 사용하는 클라이언트 응용 프로그램이 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 통신할 때, 그리고 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 사용하여 컴파일한 클라이언트가 향상된 날짜 및 시간 기능을 지원하는 서버에 명령을 전송할 때 예상되는 동작에 대해 설명합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client&#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
