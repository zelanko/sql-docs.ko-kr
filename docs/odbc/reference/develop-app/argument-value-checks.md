---
title: 인수 값 검사 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3dfee0dd00e30f6446430156617ba45a5a39b994
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63288547"
---
# <a name="argument-value-checks"></a>인수 값 검사
드라이버 관리자는 다음과 같은 유형의 인수를 확인합니다. 다른 언급이 없는 경우 드라이버 관리자 오류 인수 값에 대 한 SQL_ERROR를 반환 합니다.  
  
-   일반적으로 환경, 연결 및 문 핸들에 null 포인터 일 수 없습니다. Null 핸들을 찾으면 드라이버 관리자에서 SQL_INVALID_HANDLE을 반환 합니다.  
  
-   포인터 인수를 같은 필요한 *OutputHandlePtr* 에 **SQLAllocHandle** 하 고 *CursorName* 에서 **SQLSetCursorName**, 일 수 없습니다 null 포인터입니다.  
  
-   드라이버 관련 값을 지원 하지 않는 옵션 플래그에는 올바른 값 이어야 합니다. 예를 들어 *작업이* 에 **SQLSetPos** SQL_POSITION "," SQL_REFRESH "," SQL_UPDATE "," SQL_DELETE, "또는" SQL_ADD 여야 합니다.  
  
-   옵션 플래그의 ODBC 드라이버에서 지원 되는 버전에서 지원 되어야 합니다. 예를 들어 *정보 항목* 에 **SQLGetInfo** SQL_ASYNC_MODE (ODBC 3.0에서 도입 됨)를 사용할 수 없습니다. ODBC 2.0 드라이버를 호출 하는 경우.  
  
-   열 및 매개 변수 번호는 0 보다 크거나 함수에 따라 0 이어야 합니다. 드라이버는 현재 결과 집합 또는 SQL 문을 기반으로 이러한 인수 값의 상한값을 확인 해야 합니다.  
  
-   길이/표시기 인수 및 데이터 버퍼 길이 인수는 적절 한 값을 포함 해야 합니다. 인수에서 테이블 이름의 길이 지정 하는 예를 들어 **SQLColumns** (*NameLength3*) 해야 SQL_NTS 또는 값 0 보다 커야 합니다. *BufferLength* 에 **SQLDescribeCol** 0 보다 크거나 이어야 합니다. 드라이버가 이러한 인수를 확인 해야 할 수도 있습니다. 예를 들어,이 확인할 수 *NameLength3* 데이터 원본에 테이블 이름의 최대 길이 보다 작거나 같으면 합니다.
