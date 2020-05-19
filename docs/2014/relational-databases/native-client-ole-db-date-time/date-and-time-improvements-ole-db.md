---
title: 날짜 및 시간 기능 향상(OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
ms.assetid: 71614aaf-0fa4-4fe0-b522-68e2e0b66f43
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2d206de44f9408e932d91a0097c1228b112b05ba
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705039"
---
# <a name="date-and-time-improvements-ole-db"></a>날짜 및 시간 기능 향상(OLE DB)
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에는 새로운 날짜 및 시간 데이터 형식이 도입되었습니다. 이 섹션에서는 이러한 새로운 형식이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 확장에서 어떤 방식으로 나타나는지 설명합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]새 날짜 및 시간 데이터 형식에 대 한 Native Client 지원의 개요는 [날짜 및 시간 기능 향상](../native-client/features/date-and-time-improvements.md)을 참조 하세요. 샘플은 [향상된 날짜 및 시간 기능 사용&#40;OLE DB&#41;](../native-client-ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md)을 참조하세요.  
  
 날짜 및 시간 데이터 형식에 대한 일반적인 정보는 [datetime&#40;Transact-SQL&#41;](/sql/t-sql/data-types/datetime-transact-sql)을 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [OLE DB 날짜 및 시간 기능 향상을 위한 데이터 형식 지원](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]날짜 및 시간 데이터 형식을 지 원하는 OLE DB (Native Client) 형식에 대 한 정보를 제공 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
 [메타데이터&#40;OLE DB&#41;](../../database-engine/dev-guide/metadata-ole-db.md)  
 DBBINDING 구조체,,, 및 I에 대 한 정보를 포함 `ICommandWithParameters::GetParameterInfo` `ICommandWithParameters::SetParameterInfo` `IColumnsRowset::GetColumnsRowset` `ColumnsInfo::GetColumnInfo` 합니다. 또한 OLE DB 스키마 행 집합에 대 한 업데이트 정보를 제공 합니다.  
  
 [바인딩 및 변환&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/conversions-ole-db.md)  
 기존 데이터 형식 및 새로운 데이터 형식에 대한 서버와 클라이언트 간 변환 규칙을 설명합니다.  
  
 [향상 된 날짜 및 시간 형식에 대 한 대량 복사 변경 내용 &#40;OLE DB 및 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 대량 복사 작업을 지원하는 날짜/시간 기능 향상에 대해 설명합니다.  
  
 [날짜 및 시간 기능 향상을 위한 OLE DB API 지원](ole-db-api-support-for-date-and-time-enhancements.md)  
 향상된 날짜/시간 기능을 지원하는 OLE DB API에 대해 설명합니다.  
  
 [IRowsetFind 비교](../../relational-databases/native-client-ole-db-date-time/comparability-for-irowsetfind.md)  
 날짜/시간 형식 및 `IRowsetFind`에 대해 설명합니다.  
  
 [이전 SQL Server 버전 &#40;OLE DB의 새로운 날짜 및 시간 기능&#41;](new-date-and-time-features-with-previous-sql-server-versions-ole-db.md)  
 향상된 날짜 및 시간 기능을 사용하는 클라이언트 애플리케이션이 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 통신할 때, 그리고 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 사용하여 컴파일한 클라이언트가 향상된 날짜 및 시간 기능을 지원하는 서버에 명령을 전송할 때 예상되는 동작에 대해 설명합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client&#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
