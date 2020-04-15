---
title: 반환 코드 ODBC | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- return codes [ODBC]
- diagnostic information [ODBC], return codes
ms.assetid: e893b719-4392-476f-911a-5ed6da6f7e94
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 15e434025ed1201ca61371c2fb88e70143e131a5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304314"
---
# <a name="return-codes-odbc"></a>반환 코드 ODBC
ODBC의 각 함수는 함수의 전반적인 성공 또는 실패를 나타내는 *반환 코드라고* 하는 코드를 반환합니다. 프로그램 논리는 일반적으로 반환 코드에 기반을 둡니다.  
  
 예를 들어 다음 코드는 결과 집합의 행을 검색하기 위해 **SQLFetch를** 호출합니다. 함수의 반환 코드를 검사하여 결과 집합의 끝에 도달했는지(SQL_NO_DATA), 경고 정보가 반환되었는지(SQL_SUCCESS_WITH_INFO) 또는 오류가 발생했는지(SQL_ERROR)를 확인합니다.  
  
```  
SQLRETURN   rc;  
SQLHSTMT    hstmt;  
  
while ((rc=SQLFetch(hstmt)) != SQL_NO_DATA) {  
   if (rc == SQL_SUCCESS_WITH_INFO) {  
      // Call function to display warning information.  
   } else if (rc == SQL_ERROR) {  
      // Call function to display error information.  
      break;  
   }  
   // Process row.  
}  
```  
  
 반환 코드 SQL_INVALID_HANDLE은 항상 프로그래밍 오류를 나타내며 런타임에 발생하지 않도록 해야 합니다. 다른 모든 반환 코드는 런타임 정보를 나타내며 SQL_ERROR는 프로그래밍 오류를 나타내는 경우가 있습니다.  
  
 다음 표는 반환 코드를 정의합니다.  
  
|반환 코드|설명|  
|-----------------|-----------------|  
|SQL_SUCCESS|함수가 성공적으로 완료되었습니다. 응용 프로그램은 **SQLGetDiagField를** 호출하여 헤더 레코드에서 추가 정보를 검색합니다.|  
|SQL_SUCCESS_WITH_INFO|치명적이지 않은 오류(경고)로 함수가 성공적으로 완료되었습니다. 응용 프로그램은 추가 정보를 검색하기 위해 **SQLGetDiagRec** 또는 **SQLGetDiagField를** 호출합니다.|  
|SQL_ERROR|함수가 실패했습니다. 응용 프로그램은 추가 정보를 검색하기 위해 **SQLGetDiagRec** 또는 **SQLGetDiagField를** 호출합니다. 함수에 대한 출력 인수의 내용은 정의되지 않습니다.|  
|SQL_INVALID_HANDLE|잘못된 환경, 연결, 명령문 또는 설명자 핸들로 인해 함수가 실패했습니다. 프로그래밍 오류를 나타냅니다. **SQLGetDiagRec** 또는 **SQLGetDiagField**에서 추가 정보를 사용할 수 없습니다. 이 코드는 핸들이 null 포인터이거나 연결 핸들이 필요한 인수에 대해 문 핸들이 전달되는 경우와 같이 잘못된 형식인 경우에만 반환됩니다.|  
|SQL_NO_DATA|더 이상 데이터를 사용할 수 없습니다. 응용 프로그램은 추가 정보를 검색하기 위해 **SQLGetDiagRec** 또는 **SQLGetDiagField를** 호출합니다. 클래스 02xxx에서 하나 이상의 드라이버 정의 상태 레코드가 반환될 수 있습니다. **참고:**  ODBC 2. *x*, 이 반환 코드는 SQL_NO_DATA_FOUND 이름이 지정되었습니다.|  
|SQL_NEED_DATA|실행 시 매개 변수 데이터를 보내거나 추가 연결 정보가 필요한 경우와 같이 더 많은 데이터가 필요합니다. 응용 프로그램은 **SQLGetDiagRec** 또는 **SQLGetDiagField를** 호출하여 추가 정보를 검색합니다(있는 경우).|  
|SQL_STILL_EXECUTING|비동기적으로 시작된 함수는 여전히 실행 중입니다. 응용 프로그램은 **SQLGetDiagRec** 또는 **SQLGetDiagField를** 호출하여 추가 정보를 검색합니다(있는 경우).|
