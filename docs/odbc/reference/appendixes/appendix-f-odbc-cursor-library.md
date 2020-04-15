---
title: '부록 F: ODBC 커서 라이브러리 | 마이크로 소프트 문서'
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
ms.openlocfilehash: ec7982150bfa805c7093ab445400ef5ad1ee070c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292433"
---
# <a name="appendix-f-odbc-cursor-library"></a>부록 F: ODBC 커서 라이브러리
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 ODBC 커서 라이브러리(Odbccr32.dll)는 레벨 1 API 준수 수준을 준수하고 응용 프로그램 또는 드라이버를 통해 개발자가 재배포할 수 있는 모든 드라이버에 대해 스크롤 가능한 커서 블록을 지원합니다. 또한 커서 라이브러리는 **SELECT** 문에서 생성된 결과 집합에 대한 위치 업데이트 및 삭제 문을 지원합니다. 정적 커서와 정방향 전용 커서만 지원하지만 커서 라이브러리는 많은 응용 프로그램의 요구 사항을 충족합니다. 또한 특히 중소 규모에서 중간 크기의 결과 집합및 커서 지원이 좋지 않은 응용 프로그램에 대해 좋은 성능을 제공할 수 있습니다.  
  
 커서 라이브러리는 드라이버 관리자와 드라이버 사이에 있는 동적 링크 라이브러리(DLL)입니다. 응용 프로그램이 함수를 호출할 때 Driver Manager는 함수를 실행하거나 지정된 드라이버에서 호출하는 커서 라이브러리의 함수를 호출합니다. 지정된 연결의 경우 응용 프로그램은 커서 라이브러리가 항상 사용되는지, 드라이버가 스크롤 가능한 커서를 지원하지 않는 지 또는 사용되지 않는지 여부를 지정합니다.  
  
 커서 라이브러리는 드라이버 관리자의 드라이버로 나타납니다. 커서 라이브러리가 드라이버 관리자와 ODBC *2.x* 드라이버 사이에 있는 경우 커서 라이브러리는 ODBC *2.x* 드라이버로 나타납니다. 커서 라이브러리가 드라이버 관리자와 ODBC *3.x* 드라이버 사이에 있는 경우 커서 라이브러리는 ODBC *3.x* 드라이버로 나타납니다. 커서 라이브러리에서 발생하는 동작은 ODBC *2.x* 및 ODBC *3.x* 드라이버 모두에 대해 지원되는 바인딩 오프셋을 제외하고 작업 중인 드라이버의 버전에 따라 달라집니다.  
  
 **SQLFetch** 및 **SQLFetchScroll에서**블록 커서를 구현하기 위해 커서 라이브러리는 드라이버에서 **SQLFetch를** 반복적으로 호출합니다. 스크롤을 구현하기 위해 메모리 및 디스크 파일에서 검색한 데이터를 캐시합니다. 응용 프로그램이 새 행 집합을 요청하면 커서 라이브러리는 드라이버 또는 캐시에서 필요에 따라 검색합니다.  
  
 위치 업데이트 및 delete 문을 구현하기 위해 커서 라이브러리는 행의 각 바인딩된 열의 캐시된 값을 지정하는 **WHERE** 절을 사용하여 **UPDATE** 또는 **DELETE** 문을 생성합니다. 위치 가 있는 업데이트 문을 실행 하면 커서 라이브러리는 행 집합 버퍼의 값에서 해당 캐시를 업데이트 합니다.  
  
 ODBC 커서 라이브러리에 대한 자세한 내용은 이 부록의 다음 섹션을 참조하십시오.  
  
-   [ODBC 커서 라이브러리 사용](../../../odbc/reference/appendixes/using-the-odbc-cursor-library.md)  
  
-   [위치 지정 업데이트 및 Delete 문 실행](../../../odbc/reference/appendixes/executing-positioned-update-and-delete-statements.md)  
  
-   [커서 라이브러리 코드 예제](../../../odbc/reference/appendixes/cursor-library-code-example.md)  
  
-   [구현 노트](../../../odbc/reference/appendixes/implementation-notes.md)  
  
-   [ODBC 커서 라이브러리 오류 코드](../../../odbc/reference/appendixes/odbc-cursor-library-error-codes.md)
