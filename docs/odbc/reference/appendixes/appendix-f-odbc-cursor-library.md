---
title: '부록 f: ODBC 커서 라이브러리 | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c27845976651b0d68b91b6269a21d1cae3518df8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47649591"
---
# <a name="appendix-f-odbc-cursor-library"></a>부록 F: ODBC 커서 라이브러리
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 ODBC 커서 라이브러리 (Odbccr32.dll) 수준 1 API 적합성 수준에 맞는 모든 드라이버에 대 한 블록 스크롤 가능 커서를 지원 하며 개발자가 해당 응용 프로그램 또는 드라이버를 사용 하 여 재배포할 수 있습니다. 커서 라이브러리도 지원 위치 지정된 update 및 delete 문의 하 여 생성 된 결과 집합에 대 한 **선택** 문입니다. 만 고정 하 고 정방향 전용 커서를 지원 하기는 하지만 커서 라이브러리는 많은 응용 프로그램의 요구를 충족 합니다. 또한 중소 규모의 작은 결과 집합에 대 한 특히 및 적절 한 커서 지원 되지 않은 응용 프로그램에 대 한 좋은 성능을 제공할 수 있습니다.  
  
 커서 라이브러리는 드라이버 및 드라이버 관리자 사이 위치 하는 동적 연결 라이브러리 (DLL). 응용 프로그램 함수를 호출할 때 드라이버 관리자 함수를 실행 하거나 지정된 된 드라이버에서 호출 하는 커서 라이브러리를에서 함수를 호출 합니다. 응용 프로그램에는 지정된 된 연결에 대 한 커서 라이브러리를 항상 사용, 드라이버는 스크롤 가능 커서를 지원 하지 않는 경우 사용 또는 사용 되지 않습니다 지정 합니다.  
  
 커서 라이브러리 드라이버를 드라이버 관리자에 표시 됩니다. 커서 라이브러리에 드라이버 관리자는 ODBC 2 사이 있는 합니다. *x* 드라이버 커서 라이브러리는 ODBC 2로 나타납니다. *x* 드라이버입니다. 드라이버 관리자는 ODBC 3 사이의 커서 라이브러리가 있는 경우 *.x* 드라이버는 ODBC 3 요소로 커서 라이브러리 *.x* 드라이버입니다. 커서 라이브러리에 의해 나타나는 동작 모두 ODBC 2에 대 한 지원 되는 바인딩 오프셋을 제외 하 고, 사용 중인 드라이버의 버전에 따라 달라 집니다. *x* 고 ODBC 3. *x* 드라이버입니다.  
  
 블록 커서를 구현 하 **SQLFetch** 하 고 **SQLFetchScroll**, 커서 라이브러리를 반복적으로 호출 **SQLFetch** 드라이버에서. 스크롤을 구현 하려면 메모리에서 및 디스크 파일에서 가져온 데이터를 캐시 합니다. 응용 프로그램에서 새 행 집합을 요청 하면 커서 라이브러리의 드라이버 또는 캐시에서 필요에 따라 검색 합니다.  
  
 현재 위치 업데이트를 구현 및 delete 문을, 하려면 커서 라이브러리는 다음과 같이 생성 됩니다.는 **업데이트** 또는 **삭제** 사용 하 여 문을 **여기서** 캐시를 지정 하는 절 행에 바인딩된 각 열의 값입니다. 위치 지정된 update 문을 실행 하는 경우 커서 라이브러리는 행 집합 버퍼 값에서 해당 캐시를 업데이트 합니다.  
  
 ODBC 커서 라이브러리에 대 한 자세한 내용은이 부록의 다음 섹션을 참조 하세요.  
  
-   [ODBC 커서 라이브러리 사용](../../../odbc/reference/appendixes/using-the-odbc-cursor-library.md)  
  
-   [위치 지정 업데이트 및 Delete 문 실행](../../../odbc/reference/appendixes/executing-positioned-update-and-delete-statements.md)  
  
-   [커서 라이브러리 코드 예제](../../../odbc/reference/appendixes/cursor-library-code-example.md)  
  
-   [구현 참고 사항](../../../odbc/reference/appendixes/implementation-notes.md)  
  
-   [ODBC 커서 라이브러리 오류 코드](../../../odbc/reference/appendixes/odbc-cursor-library-error-codes.md)
