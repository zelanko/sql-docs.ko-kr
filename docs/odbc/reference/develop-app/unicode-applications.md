---
title: 유니코드 응용 프로그램 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 32b4125d0ecb1f15fab00119a8ef4ed361b6db72
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087746"
---
# <a name="unicode-applications"></a>유니코드 애플리케이션
다음 두 가지 방법 중 하나로 응용 프로그램을 유니코드 응용 프로그램으로 다시 컴파일할 수 있습니다.  
  
-   응용 프로그램의 Sqlucode .h 헤더 파일에 포함 된 유니코드 **#define** 를 포함 합니다.  
  
-   컴파일러의 유니코드 옵션을 사용 하 여 응용 프로그램을 컴파일합니다. 이 옵션은 컴파일러 마다 다릅니다.  
  
 ANSI 응용 프로그램을 유니코드 응용 프로그램으로 변환 하려면 유니코드 데이터를 저장 하 고 전달 하는 응용 프로그램을 작성 합니다. 또한 SQLPOINTER 인수를 지 원하는 함수에 대 한 호출은 바이트 수를 사용 하도록 변환 해야 합니다.  
  
 응용 프로그램이 유니코드 응용 프로그램으로 컴파일된 후 응용 프로그램에서 접미사 없이 ODBC API 함수를 호출 하는 경우 드라이버 관리자는 응용 프로그램을 유니코드 응용 프로그램으로 인식 하 고 기본 드라이버에서 유니코드를 지 원하는 경우 함수 호출을 유니코드 함수 ( *W* 접미사 포함)로 변환 합니다. ANSI 응용 프로그램에서 접미사 없이 함수를 호출 하면 드라이버 관리자는 기본 드라이버가 ANSI를 지 원하는 경우이를 ANSI로 변환 합니다. 응용 프로그램과 드라이버가 모두 같은 문자 인코딩을 지 원하는 경우 드라이버 관리자는 호출을 드라이버에 전달 합니다 (ANSI 응용 프로그램에 대 한 특정 예외 포함).  
  
 응용 프로그램에서는 접두사를 사용 하거나 사용 하지 않고 유니코드 함수 ( *W* 접미사 포함)와 ANSI *함수를 모두* 호출할 수 있습니다. 유니코드 및 ANSI 함수 호출은 혼합할 수 있습니다. 그러나 커서 라이브러리를 사용 하는 경우에는 유니코드 및 ANSI 함수 호출을 혼합할 수 없습니다. 커서 라이브러리는 혼합이 아닌 유니코드 또는 ANSI입니다.  
  
 응용 프로그램을 작성 하 여 유니코드 응용 프로그램 또는 ANSI 응용 프로그램으로 컴파일할 수 있습니다. 이 경우 문자 데이터 형식을 SQL_C_TCHAR로 선언할 수 있습니다. 응용 프로그램을 유니코드 응용 프로그램으로 컴파일하거나 ANSI 응용 프로그램으로 컴파일된 경우 SQL_C_CHAR 삽입 하는 SQL_C_WCHAR 삽입 하는 매크로입니다. 응용 프로그램 프로그래머는 응용 프로그램의 ANSI 또는 유니코드 여부에 따라 길이 인수의 크기가 변경 되기 때문에 (문자열 데이터 형식의 경우) SQLPOINTER를 인수로 사용 하는 함수를 주의 해 서 사용 해야 합니다.  
  
 함수는 유니코드 전용 함수 호출 ( *W* 접미사 포함), ANSI 전용 함수 호출 (접미사 포함) 또는 접미사가 없는 ODBC 함수 호출 *로 하는* 세 가지 방법 중 하나로 호출 될 수 있습니다. 함수의 세 가지 형태에 대 한 인수는 동일 합니다. 문자열을 가리키는 SQLCHAR \* 인수나 sqlpointer 인수를 사용 하는 함수만 UNICODE 및 ANSI 형식으로 지정 해야 합니다. **SQLBindCol** 또는 **SQLGetData** 와 같이 문자 형식으로 선언할 수 있는 인수를 포함 하는 함수의 경우 (유니코드 및 ansi 형식이 없는) 인수를 유니코드 형식, ANSI 형식 또는 C 형식 인수의 경우 SQL_C_TCHAR 매크로로 선언할 수 있습니다. 자세한 내용은 [유니코드 데이터](../../../odbc/reference/develop-app/unicode-data.md)를 참조 하세요.  
  
 응용 프로그램을 사용할 수 있는 유니코드 드라이버가 없는 경우에도 응용 프로그램을 유니코드 응용 프로그램으로 작성할 수 있습니다. 드라이버 관리자가 유니코드 함수 및 데이터 형식을 ANSI에 매핑합니다. 유니코드에서 ANSI로의 매핑을 수행 하는 데는 몇 가지 제한 사항이 있습니다. 유니코드 응용 프로그램에서 사용할 유니코드 드라이버가 있으면 성능이 향상 되 고 유니코드에서 ANSI로의 제약에 내재 된 제한이 제거 됩니다.
