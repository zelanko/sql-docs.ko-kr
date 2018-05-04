---
title: 인수 값 검사가 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- argument value checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 37a65f8b-83aa-456c-b7cf-500404abb38a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 46a947e362f9c6e614d4e28c50b7046048bf8fa0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="argument-value-checks"></a>인수 값 검사
드라이버 관리자는 다음과 같은 유형의 인수를 확인합니다. 다른 설명이 없는 한 드라이버 관리자는 오류 인수 값에 대 한 SQL_ERROR를 반환 합니다.  
  
-   일반적으로 환경, 연결 및 문 핸들 null 포인터 일 수 없습니다. Null 핸들을 찾으면 드라이버 관리자에서 SQL_INVALID_HANDLE을 반환 합니다.  
  
-   포인터 인수를 같이 필요한 *OutputHandlePtr* 에 **SQLAllocHandle** 및 *m e* 에 **SQLSetCursorName**, 될 수 없습니다 null 포인터입니다.  
  
-   드라이버 관련 값을 지원 하지 않는 옵션 플래그에는 유효한 값 이어야 합니다. 예를 들어 *작업* 에 **SQLSetPos** SQL_POSITION, SQL_REFRESH, SQL_UPDATE, SQL_DELETE, 또는 SQL_ADD 이어야 합니다.  
  
-   옵션 플래그의 ODBC 드라이버에서 지 원하는 버전에서 지원 되어야 합니다. 예를 들어 *정보 항목* 에 **SQLGetInfo** SQL_ASYNC_MODE (ODBC 3.0에서 도입) 일 수 없습니다 ODBC 2.0 드라이버를 호출할 때입니다.  
  
-   열 및 매개 변수 번호는 0 보다 큼 또는 보다 크거나 함수에 따라 0 이어야 합니다. 드라이버는 SQL 문이나 현재 결과 집합에 따라 이러한 인수 값의 상한값을 확인 해야 합니다.  
  
-   길이/표시기 인수 및 데이터 버퍼 길이 인수는 적절 한 값을 포함 해야 합니다. 인수에서 테이블 이름의 길이 지정 하는 예를 들어 **SQLColumns** (*NameLength3*) SQL_NTS 또는 값 보다 커야 0; *BufferLength* 에 **SQLDescribeCol** 보다 크거나 0 이어야 합니다. 드라이버가 이러한 인수를 확인 해야 할 수도 있습니다. 예를 들어 것 직접 확인할 수 있습니다는 *NameLength3* 가 데이터 원본에 테이블 이름의 최대 길이 보다 작거나 같으면 합니다.
