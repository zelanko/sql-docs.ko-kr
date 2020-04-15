---
title: SQLBindCol | 마이크로 소프트 문서
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 69457daccbc7868e58f91c71a48b4b25f15f5318
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302734"
---
# <a name="sqlbindcol"></a>SQLBindCol
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  일반적으로 **SQLBindCol을** 사용하여 데이터 변환을 유발할 때의 영향을 고려합니다. 바인딩 변환은 클라이언트 프로세스입니다. 예를 들어 문자 열에 바인딩된 부동 소수점 값을 검색하면 행이 인출될 때 드라이버가 부동 소수점 수에서 문자로의 변환을 로컬로 수행합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] CONVERT 함수를 사용하면 데이터 변환 비용을 서버가 부담하도록 할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 단일 문 실행에서 결과 행의 집합이 여러 개 반환될 수 있습니다. 이 경우 각 결과 집합은 개별적으로 바인딩해야 합니다. 여러 결과 집합에 대한 바인딩에 대한 자세한 내용은 [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)를 참조하십시오.  
  
 개발자는 *targetType* 값을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]사용하여 열을 특정 C 데이터 형식에 바인딩할 수 **SQL_C_BINARY.** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관련 형식에 바인딩된 열은 이식할 수 없습니다. 정의된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관련 ODBC C 데이터 형식은 DB-Library의 형식 정의와 일치하므로 애플리케이션을 이식하는 DB-Library 개발자는 이 기능을 이용할 수 있습니다.  
  
 데이터 잘림보고는 네이티브 클라이언트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC 드라이버에 대 한 비용이 많이 드는 프로세스입니다. 모든 바인딩된 데이터 버퍼의 너비가 반환되는 데이터를 수용할 만큼 넓으면 잘림을 피할 수 있습니다. 문자 데이터의 경우 문자열 종료에 기본 드라이버 동작이 사용될 때는 문자열 종결자를 수용하기 위한 공간도 너비에 포함해야 합니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **char(5)** 열을 5자 배열에 바인딩하면 가져온 모든 값에 대해 잘림됩니다. 그러나 이 열을 6개 문자의 배열에 바인딩하면 Null 종결자를 저장할 문자 요소가 제공되므로 잘림이 발생하지 않습니다. [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) 효율적으로 잘리지 않고 긴 문자 및 이진 데이터를 검색 하는 데 사용할 수 있습니다.  
  
 큰 값 데이터 형식의 경우 사용자가 제공한 버퍼가 열의 전체 값을 보유할 만큼 충분히 크지 않으면 **반환되는 SQL_SUCCESS_WITH_INFO** "문자열 데이터입니다. 오른쪽 잘림" 경고가 발행됩니다. **StrLen_or_IndPtr** 인수에는 버퍼에 저장된 chars/바이트 수가 포함됩니다.  
  
## <a name="sqlbindcol-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLBindCol 지원  
 날짜/시간 형식의 결과 열 값은 [SQL에서 C로의 변환에](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)설명된 대로 변환됩니다. 시간 및 datetimeoffset/SQL_SS_TIME2_STRUCT**및** **SQL_SS_TIMESTAMPOFFSET_STRUCT)** 열을 검색하려면 *TargetType을* **SQL_C_DEFAULT** 또는 **SQL_C_BINARY**지정해야 합니다.  
  
 자세한 내용은 [ODBC&#41;&#40;날짜 및 시간 개선 을 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)참조하십시오.  
  
## <a name="sqlbindcol-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLBindCol 지원  
 **SQLBindCol은** 대규모 CLR 사용자 정의 형식(UDT)을 지원합니다. 자세한 내용은 [큰 CLR 사용자 정의 형식 &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQLBindCol 함수](https://go.microsoft.com/fwlink/?LinkId=59327)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
