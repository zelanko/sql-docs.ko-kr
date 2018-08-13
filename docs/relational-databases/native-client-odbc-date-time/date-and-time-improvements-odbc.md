---
title: 날짜 및 시간 기능 향상 (ODBC) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- date/time [ODBC]
- ODBC, date/time improvements
ms.assetid: e31d5ca5-2103-498f-954c-1ee93e217186
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 2f1b2b021668db70e6390ccb8bcb5d724f62bcd5
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39542613"
---
# <a name="date-and-time-improvements-odbc"></a>날짜 및 시간 기능 향상(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에는 새로운 날짜 및 시간 데이터 형식이 도입되었습니다. 이 섹션에서는 이러한 새로운 형식이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 확장에서 어떤 방식으로 나타나는지 설명합니다. 에 대 한 개요 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 새 날짜 및 시간 데이터 형식에 대 한 네이티브 클라이언트 지원을 참조 하십시오. [날짜와 시간 향상](../../relational-databases/native-client/features/date-and-time-improvements.md). ODBC 날짜/시간 지원을 보여 주는 샘플을 참조 하십시오. [사용 하 여 날짜 및 시간 형식](../../relational-databases/native-client-odbc-how-to/use-date-and-time-types.md).  
  
 날짜 및 시간 데이터 형식에 대 한 자세한 내용을 보려면 [datetime &#40;Transact SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md).  
  
## <a name="in-this-section"></a>섹션 내용  
 [ODBC 날짜 및 시간 기능 향상을 위한 데이터 형식 지원](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 날짜 및 시간 데이터 형식을 지원하는 ODBC 형식에 대한 정보를 제공합니다.  
  
 [메타 데이터 &#40;ODBC&#41;](http://msdn.microsoft.com/library/99133efc-b1f2-46e9-8203-d90c324a8e4c)  
 반환 되는 구현 매개 변수 설명자 (IPD) 구현 행 설명자 (IRD) 필드와 및 열 메타 데이터에서 반환 된 정보를 설명 **SQLColumns** 및 **SQLProcedureColumns**. 또한 데이터 형식에서 반환 된 메타 데이터를 설명 **SQLGetTypeInfo**.  
  
 [날짜/시간 데이터 형식 변환 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-odbc.md)  
 datetime 값과 datetimeoffset 값을 서로 변환하는 방법에 대해 설명합니다.  
  
 [날짜 및 시간 형식에 대한 sql_variant 지원](../../relational-databases/native-client-odbc-date-time/sql-variant-support-for-date-and-time-types.md)  
 향상된 날짜 및 시간 기능을 지원하는 SQL_VARIANT 함수에 대해 설명합니다.  
  
 [향상 된 날짜 및 시간 형식에 대 한 복사본의 변경 내용을 대량 &#40;OLE DB 및 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 대량 복사 작업을 지원하는 날짜/시간 기능 향상에 대해 설명합니다.  
  
 [향상 된 날짜 및 시간 입력 동작 이전 SQL Server 버전을 사용 하 여 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/enhanced-date-and-time-type-behavior-with-previous-sql-server-versions-odbc.md)  
 향상된 날짜 및 시간 기능을 사용하는 클라이언트 응용 프로그램이 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 통신할 때, 그리고 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client에서 컴파일된 클라이언트가 향상된 날짜 및 시간 기능을 지원하는 서버에 명령을 전송할 때 예상되는 동작에 대해 설명합니다.  
  
 [향상된 날짜 및 시간 기능에 대한 ODBC API 지원](../../relational-databases/native-client-odbc-date-time/odbc-api-support-for-enhanced-date-and-time-features.md)  
 향상된 날짜 및 시간 기능을 지원하는 ODBC 함수를 소개합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
