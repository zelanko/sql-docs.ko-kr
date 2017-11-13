---
title: "부록 f: ODBC 커서 라이브러리 | Microsoft Docs"
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
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- cursor library [ODBC]
ms.assetid: a03084df-4e48-48ef-917d-4a3fae48a605
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f48f9e35793d197efc7a72600a122abc83484ed8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="appendix-f-odbc-cursor-library"></a>부록 f: ODBC 커서 라이브러리
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 ODBC 커서 라이브러리 (Odbccr32.dll) 수준 1 API 규칙 수준과 준수 하는 모든 드라이버에 대 한 블록 스크롤 가능 커서를 지원 하며 개발자가 자신의 응용 프로그램 또는 드라이버를 재배포할 수 있습니다. 커서 라이브러리도 지원 위치 지정된 update 및 delete 문을 의해 생성 된 결과 집합에 대 한 **선택** 문. 정적 및 앞 으로만 이동 가능한만 커서를 지원 하기는 하지만 커서 라이브러리는 많은 응용 프로그램의 요구를 충족 합니다. 또한 특히 중소 규모의 작은 결과 집합에 대 한 좋은 커서 지원을 없는 응용 프로그램 좋은 성능을 제공할 수 있습니다.  
  
 커서 라이브러리는 드라이버 및 드라이버 관리자 사이 있는 동적 연결 라이브러리 (DLL). 응용 프로그램에 함수를 호출할 때 드라이버 관리자는 함수를 실행 하거나 지정된 된 드라이버에서 호출 하는 커서 라이브러리에서 함수를 호출 합니다. 지정된 된 연결에 대 한 응용 프로그램 커서 라이브러리 항상 사용, 드라이버는 스크롤 가능 커서를 지원 하지 않는 경우 사용 또는 사용 되지 않았습니다.를 지정 합니다.  
  
 커서 라이브러리는 드라이버를 드라이버 관리자에 표시 됩니다. 커서 라이브러리 드라이버 관리자에서 ODBC 2 사이의 있으면 합니다. *x* 드라이버는 ODBC 2로 커서 라이브러리가 표시 됩니다. *x* 드라이버입니다. 드라이버 관리자에서 ODBC 3 사이 커서 라이브러리가 있는 경우*.x* ODBC 3으로 드라이버를 커서 라이브러리가 표시*.x* 드라이버입니다. 커서 라이브러리에서 나타나는 동작 모두 ODBC 2에 대해 지원 되는 바인딩 오프셋을 제외 하 고, 작업은 드라이버의 버전에 따라 다릅니다. *x* 및 ODBC 3. *x* 드라이버입니다.  
  
 블록 커서를 구현 하려면 **SQLFetch** 및 **SQLFetchScroll**, 커서 라이브러리를 반복적으로 호출 **SQLFetch** 드라이버에서입니다. 스크롤을 구현 하려면는 검색 한 데이터를 디스크 파일 및 메모리에 캐시 합니다. 응용 프로그램이 새 행 집합 요청을 하면 커서 라이브러리 드라이버 또는 캐시에서 필요에 따라 검색 합니다.  
  
 커서 라이브러리 구문을 하 여 위치 지정된 업데이트를 구현 및 delete 문는 **업데이트** 또는 **삭제** 문을 **여기서** 캐시 된을 지정 하는 절 행에 바인딩된 각 열 값입니다. 위치 지정된 update 문이 실행 될 때 커서 라이브러리는 행 집합 버퍼의 값에서 캐시를 업데이트 합니다.  
  
 ODBC 커서 라이브러리에 대 한 자세한 내용은이 부록의 내용의 다음 섹션을 참조 합니다.  
  
-   [ODBC 커서 라이브러리 사용](../../../odbc/reference/appendixes/using-the-odbc-cursor-library.md)  
  
-   [위치 지정 업데이트 및 Delete 문 실행](../../../odbc/reference/appendixes/executing-positioned-update-and-delete-statements.md)  
  
-   [커서 라이브러리 코드 예제](../../../odbc/reference/appendixes/cursor-library-code-example.md)  
  
-   [구현 참고 사항](../../../odbc/reference/appendixes/implementation-notes.md)  
  
-   [ODBC 커서 라이브러리 오류 코드](../../../odbc/reference/appendixes/odbc-cursor-library-error-codes.md)

