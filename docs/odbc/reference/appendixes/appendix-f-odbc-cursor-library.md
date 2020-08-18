---
description: '부록 F: ODBC 커서 라이브러리'
title: '부록 F: ODBC 커서 라이브러리 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- cursor library [ODBC]
ms.assetid: a03084df-4e48-48ef-917d-4a3fae48a605
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 325c7cdc5d2fb185ef3dbd2500a20230d90193bf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411429"
---
# <a name="appendix-f-odbc-cursor-library"></a>부록 F: ODBC 커서 라이브러리
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 ODBC 커서 라이브러리 (Odbccr32.dll)는 수준 1 API 규칙 수준을 준수 하 고 응용 프로그램이 나 드라이버를 사용 하 여 개발자가 재배포할 수 있는 모든 드라이버에 대해 스크롤 가능 커서를 차단할 수 있도록 지원 합니다. 또한 커서 라이브러리는 **SELECT** 문에서 생성 된 결과 집합에 대해 위치 지정 update 및 delete 문을 지원 합니다. 정적 및 전진 전용 커서만 지원 하지만 커서 라이브러리는 많은 응용 프로그램의 요구 사항을 충족 합니다. 또한 좋은 성능을 제공할 수 있습니다. 특히 크기가 작고 크기를 조정 하는 결과 집합의 경우 커서 지원 기능이 없는 응용 프로그램에 적합 합니다.  
  
 커서 라이브러리는 드라이버 관리자와 드라이버 사이에 있는 DLL (동적 연결 라이브러리)입니다. 응용 프로그램에서 함수를 호출 하는 경우 드라이버 관리자는 커서 라이브러리의 함수를 호출 합니다 .이 함수는 함수를 실행 하거나 지정 된 드라이버에서 호출 합니다. 지정 된 연결의 경우 응용 프로그램은 커서 라이브러리가 항상 사용 되는지 여부를 지정 합니다. 드라이버에서 스크롤 가능 커서를 지원 하지 않거나 사용 되지 않는 경우 사용 됩니다.  
  
 커서 라이브러리는 드라이버 관리자에 드라이버로 표시 됩니다. 커서 라이브러리가 드라이버 관리자와 ODBC 2.x 드라이버 사이에 있는 경우 커서 라이브러리 *는 odbc* *2.x 드라이버로 나타납니다* . 커서 라이브러리가 드라이버 관리자와 ODBC *3. x* 드라이버 사이에 있는 경우 커서 라이브러리 *는 odbc 2.x 드라이버로 나타납니다.* 커서 라이브러리에 의해 발생 하는 동작은 작업 중인 드라이버의 버전에 따라 달라 *지 며, odbc 2.x 및 odbc* *2.x 드라이버 모두* 에 대해 지원 되는 바인딩 오프셋은 제외 합니다.  
  
 **Sqlfetch** 및 **sqlfetchscroll**에서 블록 커서를 구현 하기 위해 커서 라이브러리는 드라이버에서 **sqlfetch** 를 반복적으로 호출 합니다. 스크롤을 구현 하기 위해 메모리와 디스크 파일에서 검색 한 데이터를 캐시 합니다. 응용 프로그램이 새 행 집합을 요청 하면 커서 라이브러리는 드라이버 또는 캐시에서 필요에 따라 해당 행 집합을 검색 합니다.  
  
 위치 지정 update 및 delete 문을 구현 하기 위해 커서 라이브러리는 행에서 각 바인딩된 열의 캐시 된 값을 지정 하는 **where** 절을 사용 하 여 **update** 또는 **delete** 문을 생성 합니다. 위치 지정 update 문을 실행 하면 커서 라이브러리가 행 집합 버퍼의 값에서 캐시를 업데이트 합니다.  
  
 ODBC 커서 라이브러리에 대 한 자세한 내용은이 부록의 다음 섹션을 참조 하십시오.  
  
-   [ODBC 커서 라이브러리 사용](../../../odbc/reference/appendixes/using-the-odbc-cursor-library.md)  
  
-   [위치 지정 업데이트 및 Delete 문 실행](../../../odbc/reference/appendixes/executing-positioned-update-and-delete-statements.md)  
  
-   [커서 라이브러리 코드 예제](../../../odbc/reference/appendixes/cursor-library-code-example.md)  
  
-   [구현 노트](../../../odbc/reference/appendixes/implementation-notes.md)  
  
-   [ODBC 커서 라이브러리 오류 코드](../../../odbc/reference/appendixes/odbc-cursor-library-error-codes.md)
