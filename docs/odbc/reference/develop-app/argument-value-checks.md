---
description: 인수 값 검사
title: 인수 값 확인 | Microsoft Docs
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
ms.openlocfilehash: 5dac29eea6c9a2b5f178aa233520674ea466cf48
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465955"
---
# <a name="argument-value-checks"></a>인수 값 검사
드라이버 관리자는 다음과 같은 형식의 인수를 확인 합니다. 별도로 언급 하지 않는 한 드라이버 관리자는 인수 값에서 오류에 대 한 SQL_ERROR를 반환 합니다.  
  
-   환경, 연결 및 문 핸들은 일반적으로 null 포인터 일 수 없습니다. 드라이버 관리자는 null 핸들을 찾을 때 SQL_INVALID_HANDLE을 반환 합니다.  
  
-   **SQLAllocHandle** 의 *OutputHandlePtr* 와 **SQLSetCursorName**의 *CursorName* 와 같은 필수 포인터 인수는 null 포인터 일 수 없습니다.  
  
-   드라이버 관련 값을 지원 하지 않는 옵션 플래그는 올바른 값 이어야 합니다. 예를 들어 **SQLSetPos** 의 *작업* 은 SQL_POSITION, SQL_REFRESH, SQL_UPDATE, SQL_DELETE 또는 SQL_ADD 여야 합니다.  
  
-   옵션 플래그는 드라이버에서 지 원하는 ODBC 버전에서 지원 되어야 합니다. 예를 들어 *InfoType* 는 odbc 2.0 드라이버를 호출할 때 **SQLGetInfo** 의 (odbc 3.0에 도입 됨)를 SQL_ASYNC_MODE 수 없습니다.  
  
-   열 및 매개 변수 번호는 함수에 따라 0 보다 크거나 같아야 합니다. 드라이버는 현재 결과 집합 또는 SQL 문에 따라 이러한 인수 값의 상한 값을 확인 해야 합니다.  
  
-   길이/표시기 인수 및 데이터 버퍼 길이 인수는 적절 한 값을 포함 해야 합니다. 예를 들어 **Sqlcolumns** 의 테이블 이름 길이를 지정 하는 인수 (*NameLength3*)는 SQL_NTS 또는 0 보다 큰 값 이어야 합니다. **SQLDescribeCol** 에서 *bufferlength* 는 0 보다 크거나 같아야 합니다. 드라이버는 이러한 인수를 확인 해야 할 수도 있습니다. 예를 들어 *NameLength3* 이 데이터 원본에서 테이블 이름의 최대 길이 보다 작거나 같은지 확인할 수 있습니다.
