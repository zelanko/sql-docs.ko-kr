---
title: 날짜 및 시간 기능 향상 (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
ms.assetid: 71614aaf-0fa4-4fe0-b522-68e2e0b66f43
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cd6e01f8fbacfae69e81d3779e0e1fc8b54182c7
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37410722"
---
# <a name="date-and-time-improvements-ole-db"></a>날짜 및 시간 기능 향상 (OLE DB)
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에는 새로운 날짜 및 시간 데이터 형식이 도입되었습니다. 이 섹션에서는 이러한 새로운 형식이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 확장에서 어떤 방식으로 나타나는지 설명합니다. 에 대 한 개요는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 지원 새 날짜 및 시간 데이터 형식에 대 한 참조 [날짜 및 시간 기능 향상](../native-client/features/date-and-time-improvements.md)합니다. 샘플을 보려면 [사용 하 여 향상 된 날짜 및 시간 기능 &#40;OLE DB&#41;](../native-client-ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md)합니다.  
  
 날짜 및 시간 데이터 형식에 대 한 일반적인 내용은 참조 하세요. [datetime &#40;TRANSACT-SQL&#41;](/sql/t-sql/data-types/datetime-transact-sql)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [OLE DB 날짜 및 시간 기능 향상을 위한 데이터 형식 지원](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 OLE DB에 대 한 정보를 제공 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client) 지 원하는 형식을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 날짜 및 시간 데이터 형식입니다.  
  
 [메타 데이터 &#40;OLE DB&#41;](../../database-engine/dev-guide/metadata-ole-db.md)  
 DBBINDING 구조, `ICommandWithParameters::GetParameterInfo`, `ICommandWithParameters::SetParameterInfo`, `IColumnsRowset::GetColumnsRowset` 및 I`ColumnsInfo::GetColumnInfo`에 대한 정보가 포함되어 있습니다. OLE DB 스키마 행 집합의 업데이트에 대한 정보도 제공합니다.  
  
 [바인딩 및 변환 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/conversions-ole-db.md)  
 기존 데이터 형식 및 새로운 데이터 형식에 대한 서버와 클라이언트 간 변환 규칙을 설명합니다.  
  
 [대량 복사 변경 사항으로 향상 된 날짜 및 시간 형식에 대 한 &#40;OLE DB 및 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 대량 복사 작업을 지원하는 날짜/시간 기능 향상에 대해 설명합니다.  
  
 [날짜 및 시간 기능 향상을 위한 OLE DB API 지원](ole-db-api-support-for-date-and-time-enhancements.md)  
 향상된 날짜/시간 기능을 지원하는 OLE DB API에 대해 설명합니다.  
  
 [IRowsetFind 비교](../../relational-databases/native-client-ole-db-date-time/comparability-for-irowsetfind.md)  
 날짜/시간 형식 및 `IRowsetFind`에 대해 설명합니다.  
  
 [새 날짜 및 시간 기능 이전 버전의 SQL Server 사용 하 여 &#40;OLE DB&#41;](new-date-and-time-features-with-previous-sql-server-versions-ole-db.md)  
 향상된 날짜 및 시간 기능을 사용하는 클라이언트 응용 프로그램이 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 통신할 때, 그리고 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 사용하여 컴파일한 클라이언트가 향상된 날짜 및 시간 기능을 지원하는 서버에 명령을 전송할 때 예상되는 동작에 대해 설명합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client&#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
