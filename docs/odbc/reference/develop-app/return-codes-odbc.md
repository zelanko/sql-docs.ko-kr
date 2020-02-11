---
title: 반환 코드 ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e5f780f9abc47a367a1825d51b12159292ace5da
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020424"
---
# <a name="return-codes-odbc"></a>반환 코드 ODBC
ODBC의 각 함수는 *반환 코드* 라고 하는 코드를 반환 합니다 .이 코드는 함수의 전체 성공 또는 실패를 나타냅니다. 프로그램 논리는 일반적으로 반환 코드에 기반을 둡니다.  
  
 예를 들어 다음 코드는 **Sqlfetch** 를 호출 하 여 결과 집합에서 행을 검색 합니다. 함수의 반환 코드를 검사 하 여 결과 집합의 끝에 도달 했는지 (SQL_NO_DATA), 경고 정보가 반환 되었는지 (SQL_SUCCESS_WITH_INFO) 또는 오류가 발생 한 경우 (SQL_ERROR)를 확인 합니다.  
  
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
  
 다음 표에서는 반환 코드를 정의 합니다.  
  
|반환 코드|Description|  
|-----------------|-----------------|  
|SQL_SUCCESS|함수가 성공적으로 완료 되었습니다. 응용 프로그램은 **SQLGetDiagField** 를 호출 하 여 헤더 레코드에서 추가 정보를 검색 합니다.|  
|SQL_SUCCESS_WITH_INFO|함수가 정상적으로 완료 되었습니다. 심각 하지 않은 오류가 발생 했습니다 (경고). 응용 프로그램은 **SQLGetDiagRec** 또는 **SQLGetDiagField** 를 호출 하 여 추가 정보를 검색 합니다.|  
|SQL_ERROR|함수가 실패 했습니다. 응용 프로그램은 **SQLGetDiagRec** 또는 **SQLGetDiagField** 를 호출 하 여 추가 정보를 검색 합니다. 함수에 대 한 출력 인수의 내용이 정의 되어 있지 않습니다.|  
|SQL_INVALID_HANDLE|잘못 된 환경, 연결, 문 또는 설명자 핸들로 인해 함수가 실패 했습니다. 이는 프로그래밍 오류를 나타냅니다. **SQLGetDiagRec** 또는 **SQLGetDiagField**에서 추가 정보를 사용할 수 없습니다. 이 코드는 핸들이 null 포인터 이거나 잘못 된 형식인 경우에만 반환 됩니다. 예를 들어, 연결 핸들이 필요한 인수에 대해 문 핸들이 전달 되는 경우에 해당 합니다.|  
|SQL_NO_DATA|사용할 수 있는 데이터가 더 이상 없습니다. 응용 프로그램은 **SQLGetDiagRec** 또는 **SQLGetDiagField** 를 호출 하 여 추가 정보를 검색 합니다. 02xxx 클래스의 드라이버 정의 상태 레코드 중 하나 이상이 반환 될 수 있습니다. **참고:**  ODBC 2. *x*,이 반환 코드의 이름은 SQL_NO_DATA_FOUND입니다.|  
|SQL_NEED_DATA|실행 시 매개 변수 데이터를 전송 하는 경우와 같은 추가 데이터가 필요 하거나 추가 연결 정보가 필요 합니다. 응용 프로그램은 **SQLGetDiagRec** 또는 **SQLGetDiagField** 를 호출 하 여 추가 정보 (있는 경우)를 검색 합니다.|  
|SQL_STILL_EXECUTING|비동기적으로 시작 된 함수가 아직 실행 되 고 있습니다. 응용 프로그램은 **SQLGetDiagRec** 또는 **SQLGetDiagField** 를 호출 하 여 추가 정보 (있는 경우)를 검색 합니다.|
