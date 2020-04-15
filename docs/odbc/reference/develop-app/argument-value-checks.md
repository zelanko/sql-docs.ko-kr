---
title: 인수 값 검사 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- argument value checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 37a65f8b-83aa-456c-b7cf-500404abb38a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6c6e4de16c4a1a80be893acbc7a1993b375f2fee
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298828"
---
# <a name="argument-value-checks"></a>인수 값 검사
드라이버 관리자는 다음과 같은 유형의 인수를 확인합니다. 달리 명시되지 않는 한 드라이버 관리자는 인수 값의 오류에 대해 SQL_ERROR 반환합니다.  
  
-   환경, 연결 및 명령문 핸들은 일반적으로 null 포인터가 될 수 없습니다. 드라이버 관리자는 null 핸들을 찾을 때 SQL_INVALID_HANDLE 반환합니다.  
  
-   **SQLAllocHandle의** *OutputHandlePtr* 및 **SQLSetCursorName의** *커서Name과* 같은 필수 포인터 인수는 null 포인터가 될 수 없습니다.  
  
-   드라이버 관련 값을 지원하지 않는 옵션 플래그는 법적 값이어야 합니다. 예를 들어 **SQLSetPos의** *작업은* SQL_POSITION, SQL_REFRESH, SQL_UPDATE, SQL_DELETE 또는 SQL_ADD 되어야 합니다.  
  
-   옵션 플래그는 드라이버에서 지원하는 ODBC 버전에서 지원되어야 합니다. 예를 들어 **SQLGetInfo의** *InfoType은* ODBC 2.0 드라이버를 호출할 때 SQL_ASYNC_MODE 수 없습니다(ODBC 3.0에 도입).  
  
-   열 및 매개 변수 번호는 함수에 따라 0보다 크거나 0보다 크거나 같어야 합니다. 드라이버는 현재 결과 집합 또는 SQL 문을 기반으로 이러한 인수 값의 상한을 확인해야 합니다.  
  
-   길이/표시기 인수 및 데이터 버퍼 길이 인수에는 적절한 값이 포함되어야 합니다. 예를 들어*SQLColumns(NameLength3)에서*테이블 **SQLColumns** 이름의 길이를 지정하는 인수는 SQL_NTS 값이어야 하며 값이 0보다 커야 합니다. **SQLDescribeCol의** *버퍼길이는* 0보다 크거나 같아야 합니다. 드라이버는 이러한 인수를 확인해야 할 수도 있습니다. 예를 들어 *NameLength3가* 데이터 원본의 테이블 이름의 최대 길이보다 적거나 같음을 확인할 수 있습니다.
