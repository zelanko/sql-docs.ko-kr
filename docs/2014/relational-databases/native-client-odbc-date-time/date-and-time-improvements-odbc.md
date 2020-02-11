---
title: 날짜 및 시간 기능 향상 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- date/time [ODBC]
- ODBC, date/time improvements
ms.assetid: e31d5ca5-2103-498f-954c-1ee93e217186
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d56689bb045a6540bfdfbb9c7147dc34db110bde
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63207009"
---
# <a name="date-and-time-improvements-odbc"></a>날짜 및 시간 기능 향상(ODBC)
  
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에는 새로운 날짜 및 시간 데이터 형식이 도입되었습니다. 이 섹션에서는 이러한 새로운 형식이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 확장에서 어떤 방식으로 나타나는지 설명합니다. 새 날짜 및 시간 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식에 대 한 Native Client 지원에 대 한 개요는 [날짜 및 시간 기능 향상](../native-client/features/date-and-time-improvements.md)을 참조 하세요. ODBC 날짜/시간 지원을 보여 주는 예제는 [날짜 및 시간 형식 사용](../native-client-odbc-how-to/use-date-and-time-types.md)을 참조 하세요.  
  
 날짜 및 시간 데이터 형식에 대 한 일반적인 정보는 [datetime &#40;transact-sql&#41;](/sql/t-sql/data-types/datetime-transact-sql)을 참조 하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [ODBC 날짜 및 시간 기능 향상을 위한 데이터 형식 지원](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 날짜 및 시간 데이터 형식을 지원하는 ODBC 형식에 대한 정보를 제공합니다.  
  
 [ODBC&#41;&#40;메타 데이터](../../database-engine/dev-guide/metadata-odbc.md)  
 IPD(구현 매개 변수 설명자)와 IRD(구현 행 설명자) 필드에서 반환되는 정보와 `SQLColumns` 및 `SQLProcedureColumns`에서 반환되는 열 메타데이터에 대해 설명합니다. 또한 `SQLGetTypeInfo`에서 반환되는 데이터 형식 메타데이터에 대해서도 설명합니다.  
  
 [ODBC&#41;&#40;datetime 데이터 형식 변환](datetime-data-type-conversions-odbc.md)  
 datetime 값과 datetimeoffset 값을 서로 변환하는 방법에 대해 설명합니다.  
  
 [날짜 및 시간 형식에 대한 sql_variant 지원](sql-variant-support-for-date-and-time-types.md)  
 향상된 날짜 및 시간 기능을 지원하는 SQL_VARIANT 함수에 대해 설명합니다.  
  
 [향상 된 날짜 및 시간 형식에 대 한 대량 복사 변경 내용 &#40;OLE DB 및 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 대량 복사 작업을 지원하는 날짜/시간 기능 향상에 대해 설명합니다.  
  
 [이전 SQL Server 버전의 향상 된 날짜 및 시간 형식 동작 (ODBC&#41;&#40;](enhanced-date-and-time-type-behavior-with-previous-sql-server-versions-odbc.md)  
 향상된 날짜 및 시간 기능을 사용하는 클라이언트 애플리케이션이 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 통신할 때, 그리고 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client에서 컴파일된 클라이언트가 향상된 날짜 및 시간 기능을 지원하는 서버에 명령을 전송할 때 예상되는 동작에 대해 설명합니다.  
  
 [향상된 날짜 및 시간 기능에 대한 ODBC API 지원](odbc-api-support-for-enhanced-date-and-time-features.md)  
 향상된 날짜 및 시간 기능을 지원하는 ODBC 함수를 소개합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;SQL Server Native Client &#40;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
