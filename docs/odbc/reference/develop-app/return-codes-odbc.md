---
title: "반환 코드 ODBC | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- return codes [ODBC]
- diagnostic information [ODBC], return codes
ms.assetid: e893b719-4392-476f-911a-5ed6da6f7e94
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b997bfd1cc338f9c7a9dbb4b1b5b1ce851e71072
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="return-codes-odbc"></a>ODBC 반환 코드
ODBC에서 각 함수 라고 하는 코드를 반환 합니다. 해당 *코드를 반환* 전반적인 성공 또는 실패는 함수의 나타냅니다. 프로그램 논리는 일반적으로 반환 코드에 기반을 둡니다.  
  
 예를 들어 다음 코드 호출 **SQLFetch** 결과 집합의 행을 검색 합니다. 반환 코드 (SQL_ERROR)에 오류가 발생 하거나 모든 경고 정보 (SQL_SUCCESS_WITH_INFO)를 반환 된 경우 결과 집합의 끝 (SQL_NO_DATA)에 도달한 경우를 결정 하는 함수를 확인 합니다.  
  
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
  
 다음 표에서 반환 코드를 정의합니다.  
  
|반환 코드|Description|  
|-----------------|-----------------|  
|SQL_SUCCESS|함수는 성공적으로 완료 되었습니다. 응용 프로그램 호출 **SQLGetDiagField** 헤더 레코드에서 추가 정보를 검색 합니다.|  
|SQL_SUCCESS_WITH_INFO|성공적으로 치명적이 지 않은 오류 (경고)와 함께 가능 완료 하는 함수입니다. 응용 프로그램 호출 **SQLGetDiagRec** 또는 **SQLGetDiagField** 추가 정보를 검색 합니다.|  
|SQL_ERROR|함수가 실패 했습니다. 응용 프로그램 호출 **SQLGetDiagRec** 또는 **SQLGetDiagField** 추가 정보를 검색 합니다. 출력 매개 변수는 함수에의 내용을 정의 되지 않습니다.|  
|SQL_INVALID_HANDLE|잘못 된 환경, 연결, 문 또는 설명자 핸들 인해 함수가 실패 했습니다. 프로그래밍 오류를 나타냅니다. 추가 정보 없음에서 사용할 수는 **SQLGetDiagRec** 또는 **SQLGetDiagField**합니다. 이 코드는 핸들이 null 포인터 또는 문 핸들 연결 핸들을 필요로 하는 인수에 대해 전달 되 면 같은 잘못 된 형식이 고, 경우에 반환 됩니다.|  
|SQL_NO_DATA|데이터가 더 이상 사용할 수 없었습니다. 응용 프로그램 호출 **SQLGetDiagRec** 또는 **SQLGetDiagField** 추가 정보를 검색 합니다. 클래스 02xxx에서 하나 이상의 드라이버에서 정의 된 상태 레코드를 반환할 수 있습니다. **참고:** Odbc 2.* x*, 이렇게 하면 코드 SQL_NO_DATA_FOUND 변수의 이름이 반환 합니다.|  
|SQL_NEED_DATA|더 많은 데이터와 같이 필요한 실행 시 매개 변수 데이터를 보내면 또는 추가 연결 정보가 필요 합니다. 응용 프로그램 호출 **SQLGetDiagRec** 또는 **SQLGetDiagField** 있는 경우 추가 정보를 검색할 수 있습니다.|  
|SQL_STILL_EXECUTING|비동기적으로 시작 하는 함수는 계속 실행 됩니다. 응용 프로그램 호출 **SQLGetDiagRec** 또는 **SQLGetDiagField** 있는 경우 추가 정보를 검색할 수 있습니다.|

