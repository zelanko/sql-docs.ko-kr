---
title: 유니코드 응용 프로그램 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], compiling as Unicode application
- Unicode [ODBC], functions
- compiling Unicode applications [ODBC]
- functions [ODBC], Unicode functions
ms.assetid: 7986c623-2792-4e77-bfee-c86cbf84f08d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94bd5211c878904453624adb2acd0fe435ebc812
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298949"
---
# <a name="unicode-applications"></a>유니코드 애플리케이션
다음 두 가지 방법 중 하나로 응용 프로그램을 유니코드 응용 프로그램으로 다시 컴파일할 수 있습니다.  
  
-   응용 프로그램의 Sqlucode.h 헤더 파일에 포함된 유니코드 **#define** 포함합니다.  
  
-   컴파일러의 유니코드 옵션을 사용 하 고 응용 프로그램을 컴파일합니다. 이 옵션은 컴파일러마다 다릅니다.  
  
 ANSI 응용 프로그램을 유니코드 응용 프로그램으로 변환하려면 유니코드 데이터를 저장하고 전달할 응용 프로그램을 작성합니다. 또한 SQLPOINTER 인수를 지원하는 함수에 대한 호출을 바이트 수를 사용하도록 변환해야 합니다.  
  
 응용 프로그램이 유니코드 응용 프로그램으로 컴파일된 후 응용 프로그램이 ODBC API 함수(접미사 없이)를 호출하는 경우 드라이버 관리자는 응용 프로그램을 유니코드 응용 프로그램으로 인식하고 기본 드라이버가 유니코드를 지원하는 경우 함수 호출을 유니코드 *함수(W* 접미사 사용)로 변환합니다. ANSI 응용 프로그램이 접미사 없이 함수 호출을 하면 기본 드라이버가 ANSI를 지원하는 경우 드라이버 관리자는 ANSI로 변환합니다. 응용 프로그램과 드라이버가 동일한 문자 인코딩을 지원하는 경우 드라이버 관리자는 ANSI 응용 프로그램에 대한 특정 예외를 제외하고 호출을 드라이버로 전달합니다.  
  
 응용 프로그램은 유니코드 *함수(W* 접미사 사용)와 ANSI *함수(A* 접미사 유무)를 모두 호출할 수 있습니다. 유니코드 및 ANSI 함수 호출을 혼합할 수 있습니다. 그러나 커서 라이브러리를 사용할 경우 유니코드 및 ANSI 함수 호출을 혼합할 수 없습니다. 커서 라이브러리는 유니코드 또는 ANSI이며 혼합물이 아닙니다.  
  
 응용 프로그램을 유니코드 응용 프로그램 또는 ANSI 응용 프로그램으로 컴파일할 수 있도록 작성할 수 있습니다. 이 경우 문자 데이터 형식을 SQL_C_TCHAR 선언할 수 있습니다. 응용 프로그램이 유니코드 응용 프로그램으로 컴파일되는 경우 SQL_C_WCHAR 삽입하거나 ANSI 응용 프로그램으로 컴파일되는 경우 SQL_C_CHAR 삽입하는 매크로입니다. 응용 프로그램 프로그래머는 길이 인수의 크기가 응용 프로그램이 ANSI인지 유니코드인지에 따라 길이 인수의 크기가 변경되므로 SQLPOINTER를 인수로 하는 함수에 주의해야 합니다.  
  
 함수는 유니코드 전용 함수 *호출(W* 접미사 사용), ANSI 전용 함수 *호출(A* 접미사 사용) 또는 접미사가 없는 ODBC 함수 호출의 세 가지 방법 중 하나로 호출할 수 있습니다. 함수의 세 가지 형식에 대한 인수는 동일합니다. 문자열을 가리키는 SQLCHAR \* 인수 또는 SQLPOINTER 인수를 가진 함수만 유니코드 및 ANSI 양식이 필요합니다. **SQLBindCol** 또는 **SQLGetData(유니코드** 및 ANSI 양식이 없는)와 같이 문자 유형으로 선언할 수 있는 인수가 있는 함수의 경우 인수를 유니코드 유형, ANSI 형식 또는 C 형식 인수의 경우 SQL_C_TCHAR 매크로로 선언할 수 있습니다. 자세한 내용은 [유니코드 데이터](../../../odbc/reference/develop-app/unicode-data.md)를 참조하십시오.  
  
 응용 프로그램을 사용할 수 있는 유니코드 드라이버가 없는 경우에도 응용 프로그램을 유니코드 응용 프로그램으로 작성할 수 있습니다. 드라이버 관리자는 유니코드 함수 및 데이터 형식을 ANSI에 매핑합니다. 수행 할 수있는 ANSI 매핑에 유니 코드에 몇 가지 제한이 있습니다. 유니코드 응용 프로그램이 사용할 유니코드 드라이버가 존재하면 성능이 향상되고 ANSI 매핑에 유니코드에 내재된 제한 사항이 제거됩니다.
