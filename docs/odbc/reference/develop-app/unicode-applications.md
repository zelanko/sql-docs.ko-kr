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
manager: craigg
ms.openlocfilehash: 7fc9cb98837d206d5279d1f14d4a57ce56782759
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62633383"
---
# <a name="unicode-applications"></a>유니코드 애플리케이션
두 가지 방법 중 하나에서 유니코드 응용 프로그램으로 응용 프로그램을 다시 컴파일할 수 있습니다.  
  
-   유니코드를 포함 **#define** 에 응용 프로그램에는 Sqlucode.h 헤더 파일이 포함 되어 있습니다.  
  
-   컴파일러의 유니코드 옵션을 사용 하 여 응용 프로그램을 컴파일하십시오. (이 옵션은 다를 수 다른 컴파일러에 대 한 합니다.)  
  
 유니코드 응용 프로그램에는 ANSI 응용 프로그램으로 변환 하려면 저장 하 고 유니코드 데이터를 전달 하도록 응용 프로그램을 작성 합니다. 또한 대 SQLPOINTER 인수를 지 원하는 함수를 호출 하는 바이트 수를 사용 하도록 변환 되어야 합니다.  
  
 드라이버 관리자 유니코드 응용 프로그램으로 응용 프로그램을 인식 하 고 변환 함수 호출을 유니코드 (사용 하 여 함수를 프로그램이컴파일되면유니코드응용프로그램의경우응용프로그램(접미사)없이ODBCAPI함수를호출하는경우 *W* 접미사) 기본 드라이버에서 유니코드를 지 원하는 경우. ANSI 응용 프로그램 함수를 접미사가 없는 호출 하면 드라이버 관리자 변환 ANSI 기본 드라이버 ANSI를 지원 합니다. 응용 프로그램 및 드라이버를 모두 동일한 문자 인코딩을 지원 하는 경우 ANSI 응용 프로그램에 대 한 특정 예외) (사용 하 여 드라이버를 통해 호출 드라이버 관리자에 전달 합니다.  
  
 응용 프로그램 모두 유니코드 함수를 호출할 수 있습니다 (사용 하 여 합니다 *W* 접미사) 및 ANSI 함수 (유무에 관계 없이 합니다 *는* 접미사). 유니코드 및 ANSI 함수 호출을 혼합할 수 있습니다. 그러나 커서 라이브러리를 사용할 경우 유니코드 및 ANSI 함수 호출 혼합할 수 없습니다. 커서 라이브러리는 유니코드 또는 ANSI 혼합은 아님입니다.  
  
 응용 프로그램을 유니코드 또는 ANSI 응용 프로그램으로 컴파일할 수 있도록 응용 프로그램을 작성할 수 있습니다. 이 경우 문자 데이터 형식 SQL_C_TCHAR로 선언할 수 있습니다. 이 응용 프로그램은 유니코드 응용 프로그램으로 컴파일되거나 ANSI 응용 프로그램으로 컴파일된 경우 SQL_C_CHAR 삽입 SQL_C_WCHAR 삽입 하는 매크로입니다. 응용 프로그램 프로그래머가 반드시 대 SQLPOINTER 해당 인수로 사용 하는 함수의 (문자열 데이터 형식)에 대 한 길이 인수 크기 변경 되므로 ANSI 또는 유니코드 응용 프로그램 인지에 따라 합니다.  
  
 세 가지 방법 중 하나에서 함수를 호출할 수 있습니다: 유니코드 전용 함수 호출으로 (사용 하 여는 *W* 접미사), ANSI 전용 함수 호출으로 (사용 하 여 합니다 *는* 접미사), 또는 없는 접미사를 사용 하 여 ODBC 함수 호출 합니다. 함수의 세 가지 형식에 대 한 인수는 동일 합니다. SQLCHAR 사용 하 여 해당 함수만 \* 인수나 대 SQLPOINTER 인수 문자열을 가리키는 유니코드 및 ANSI 양식이 필요 합니다. 와 같은 문자 형식으로 선언할 수 있는 인수가 있는 함수에 대 한 **SQLBindCol** 하거나 **SQLGetData** (하는 없는 경우 유니코드 및 ANSI 형태)를 유니코드 형식으로 인수를 선언할 수 있습니다 ANSI 형식으로 또는 형식 인수를 SQL_C_TCHAR 매크로 C의 경우. 자세한 내용은 [유니코드 데이터](../../../odbc/reference/develop-app/unicode-data.md)입니다.  
  
 유니코드 드라이버가 없는와 작동 하도록 하기 위해 사용할 수 있는 경우에 유니코드 응용 프로그램으로 응용 프로그램을 작성할 수 있습니다. 드라이버 관리자 ANSI로 유니코드 함수 및 데이터 형식을 매핑합니다. 에 유니코드에서 ANSI 매핑 수행할 수 있는 몇 가지 제한이 있습니다. 사용 하도록 유니코드 응용 프로그램에 대 한 유니코드 드라이버의 존재 여부 성능이 향상 됩니다 및 ANSI 매핑에 유니코드에 내재 된 제한 사항이 제거 됩니다.
