---
title: 저장소 할당 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- column-wise binding [ODBC]
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- SQLBindCol function
- storing data [ODBC]
- result sets [ODBC], storage
- SQL Server Native Client ODBC driver, data storage
- row-wise binding
- binding result sets [SQL Server Native Client]
- array binding
ms.assetid: 11c81955-5300-495f-925f-9256f2587b58
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0aefbfdeb984aa6b384c5c123ed69ec4fdaa41ba
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63200035"
---
# <a name="assigning-storage"></a>스토리지 할당
  애플리케이션에서 SQL 문 실행 전이나 후에 결과의 스토리지를 할당할 수 있습니다. 애플리케이션에서 먼저 SQL 문을 준비하거나 실행하는 경우 결과의 스토리지를 할당하기 전에 결과 집합을 조회할 수 있습니다. 예를 들어 결과 집합을 알 수 없는 경우 애플리케이션에서는 결과의 스토리지를 할당하기 전에 열의 수를 검색해야 합니다.  
  
 데이터 열에 대 한 저장소를 연결 하기 위해 응용 프로그램은 [SQLBindCol](../native-client-odbc-api/sqlbindcol.md)를 호출 하 고이를 전달 합니다.  
  
-   데이터를 변환할 데이터 형식  
  
-   데이터에 대한 출력 버퍼의 주소  
  
     애플리케이션에서는 이 버퍼를 할당해야 하며, 이 버퍼는 변환되는 형식의 데이터를 저장할 수 있을 만큼 커야 합니다.  
  
-   출력 버퍼의 길이  
  
     반환된 데이터가 C에서 정수, 실수 또는 날짜 구조와 같이 고정 폭인 경우 이 값은 무시됩니다.  
  
-   사용 가능한 데이터의 바이트 수를 반환할 스토리지 버퍼의 주소  
  
 또한 애플리케이션에서는 결과 집합 행을 블록 단위로 인출할 수 있도록 결과 집합 열을 프로그램 변수 배열에 바인딩할 수도 있습니다. 배열 바인딩에는 다음과 같은 두 가지 유형이 있습니다.  
  
-   열 단위 바인딩은 각 열이 고유한 변수 배열에 바인딩되면 완료됩니다.  
  
     열 단위 바인딩은 *특성* 을 SQL_ATTR_ROW_BIND_TYPE *로 설정 하 고 SQL_BIND_BY_COLUMN* 로 설정 된 [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md) 를 호출 하 여 지정 합니다. 모든 배열의 요소 수가 동일해야 합니다.  
  
-   행 단위 바인딩은 SQL 문의 모든 매개 변수가 매개 변수의 개별 변수를 포함하는 구조체 배열에 하나의 단위로 바인딩되면 완료됩니다.  
  
     행 단위 바인딩은 *특성* 을 SQL_ATTR_ROW_BIND_TYPE로 설정 하 고 *valueptr* 을 결과 집합 열을 받는 변수를 포함 하는 구조체의 크기로 설정 하 여 **SQLSetStmtAttr** 를 호출 하 여 지정 합니다.  
  
 또한 애플리케이션에서는 SQL_ATTR_ROW_ARRAY_SIZE를 열 또는 행 배열의 요소 수로 설정하고 SQL_ATTR_ROW_STATUS_PTR 및 SQL_ATTR_ROWS_FETCHED_PTR을 설정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;결과 처리](processing-results-odbc.md)  
  
  
