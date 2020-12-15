---
description: SQLBindCol
title: SQLBindCol | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLBindCol function
ms.assetid: fbd7ba20-d917-4ca9-b018-018ac6af9f98
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f891ab146a80c99462be9c2634d687c61fe52b99
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97469554"
---
# <a name="sqlbindcol"></a>SQLBindCol
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  일반적으로 **SQLBindCol** 를 사용 하 여 데이터를 변환 하는 경우의 의미를 고려 하십시오. 바인딩 변환은 클라이언트 프로세스입니다. 예를 들어 문자 열에 바인딩된 부동 소수점 값을 검색하면 행이 인출될 때 드라이버가 부동 소수점 수에서 문자로의 변환을 로컬로 수행합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] CONVERT 함수를 사용하면 데이터 변환 비용을 서버가 부담하도록 할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 단일 문 실행에서 결과 행의 집합이 여러 개 반환될 수 있습니다. 이 경우 각 결과 집합은 개별적으로 바인딩해야 합니다. 여러 결과 집합을 바인딩하는 방법에 대 한 자세한 내용은 [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)를 참조 하세요.  
  
 개발자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **SQL_C_BINARY** *TargetType* 값을 사용 하 여 특정 C 데이터 형식에 열을 바인딩할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관련 형식에 바인딩된 열은 이식할 수 없습니다. 정의된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관련 ODBC C 데이터 형식은 DB-Library의 형식 정의와 일치하므로 애플리케이션을 이식하는 DB-Library 개발자는 이 기능을 이용할 수 있습니다.  
  
 보고 데이터 잘림은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 드라이버에 대 한 비용이 많이 드는 프로세스입니다. 모든 바인딩된 데이터 버퍼의 너비가 반환되는 데이터를 수용할 만큼 넓으면 잘림을 피할 수 있습니다. 문자 데이터의 경우 문자열 종료에 기본 드라이버 동작이 사용될 때는 문자열 종결자를 수용하기 위한 공간도 너비에 포함해야 합니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **char (5)** 열을 5 개 문자의 배열에 바인딩하면 인출 되는 모든 값에 대해 잘림이 발생 합니다. 그러나 이 열을 6개 문자의 배열에 바인딩하면 Null 종결자를 저장할 문자 요소가 제공되므로 잘림이 발생하지 않습니다. [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) 는 잘림 없이 긴 문자 및 이진 데이터를 효율적으로 검색 하는 데 사용할 수 있습니다.  
  
 Large value 데이터 형식의 경우 사용자가 제공한 버퍼가 열의 전체 값을 저장 하기에 충분히 크지 않은 경우 **SQL_SUCCESS_WITH_INFO** 반환 되 고 "문자열 데이터; 오른쪽 잘림 "경고가 발생 합니다. **StrLen_or_IndPtr** 인수에는 버퍼에 저장 된 문자/바이트 수가 포함 됩니다.  
  
## <a name="sqlbindcol-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLBindCol 지원  
 날짜/시간 형식의 결과 열 값은 [SQL에서 C로 변환](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)에 설명 된 대로 변환 됩니다. Time 및 datetimeoffset 열을 해당 구조 (**SQL_SS_TIME2_STRUCT** 및 **SQL_SS_TIMESTAMPOFFSET_STRUCT**)로 검색 하려면 *TargetType* 을 **SQL_C_DEFAULT** 또는 **SQL_C_BINARY** 로 지정 해야 합니다.  
  
 자세한 내용은 [ODBC&#41;&#40;날짜 및 시간 향상 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)을 참조 하세요.  
  
## <a name="sqlbindcol-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLBindCol 지원  
 **SQLBindCol** 는 많은 CLR udt (사용자 정의 형식)를 지원 합니다. 자세한 내용은 [ODBC&#41;&#40;대량 CLR User-Defined 형식 ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLBindCol 함수](../../odbc/reference/syntax/sqlbindcol-function.md)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
