---
title: 데이터 및 C 문자열 문자 | Microsoft Docs
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
- data buffers [ODBC], length
- data buffers [ODBC], character data
- buffers [ODBC], C strings
- buffers [ODBC], character data
- character data and buffers [ODBC]
- length of data buffers [ODBC]
- data buffers [ODBC], C strings
- buffers [ODBC], length
- C strings and buffers [ODBC]
ms.assetid: 3a141cb4-229d-4027-9349-615cb2995e36
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c23f124aeba138e0ffecc432f28fde4c11c7d1b2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32912388"
---
# <a name="character-data-and-c-strings"></a>문자 데이터 및 C 문자열
가변 길이 문자 데이터 (예: 열 이름, 동적 매개 변수 및 문자열 특성 값)를 참조 하는 입력된 매개 변수는 연결 된 길이 매개 변수를 갖습니다. 응용 프로그램이 종료 C에서 일반적인 경우 처럼 null 문자를 사용 하 여 문자열, 바이트 (null 종결자 제외)는 문자열의 길이 또는 SQL_NTS (Null-Terminated 문자열)를 인수로 제공 합니다. 음수가 아닌 길이 인수는 연결된 문자열의 실제 길이 지정합니다. 길이 인수에는 NULL 값을와 다릅니다. 길이가 0 인 문자열을 지정 하려면 0 일 수 있습니다. 음수 값 SQL_NTS null 종결 문자를 배치 하 여 문자열의 길이 확인 하는 드라이버를 보냅니다.  
  
 문자 데이터는 응용 프로그램에는 드라이버에서 반환 되 면 드라이버 해야 항상 null로 종료 것입니다. 이렇게 하면 응용 프로그램 여부를 문자열 또는 문자 배열의 데이터를 처리 하려면 선택 합니다. 응용 프로그램 버퍼를 충분히 모든 문자 데이터를 반환할 수 없는 경우 드라이버는 null 종결 문자에 따라 필요한 바이트 수를 뺀 버퍼의 바이트 길이에, 잘린된 데이터를 null로 끝냅니다 잘리고에 저장 된 버퍼입니다. 따라서 응용 프로그램이 문자 데이터를 검색 하는 데 사용 되는 버퍼에 null 종결 문자에 대 한 추가 공간이 할당 항상 해야 합니다. 예를 들어 51 바이트 버퍼 데이터의 50 문자를 검색 하려면 필요 합니다.  
  
 특별 한 주의 해야 응용 프로그램과 보내거나 긴 문자 데이터에 사용 하 여 파트를 검색 하는 경우 드라이버에서 **SQLPutData** 또는 **SQLGetData**합니다. 데이터를 일련의 null로 끝나는 문자열로로 전달 되 면 데이터를 다시 조합 수 전에이 문자열에 대해 null 종료 문자를 제거 해야 합니다.  
  
 문자 데이터 및 C 문자열 ODBC 프로그래머의 수가 혼동 있어야 합니다. 이 문제가 발생 하는 ODBC 함수를 정의 하는 경우에 C 언어를 사용 하는 아티팩트입니다. ODBC 드라이버 또는 응용 프로그램 다른 언어를 사용 하는 경우-ODBC는 언어 독립-이러한 혼동은 발생할 가능성이 더 낮아집니다.  
  
 문자 데이터를 보유 하는 C 문자열 사용 되는 경우 null 종결 문자는 데이터의 일부로 간주 되지 않습니다 및 바이트 길이의 일부로 계산 되지 않습니다. 예를 들어 "ABC\0" C 문자열 또는 문자 배열의 {'A', 'B', 'C'을 (를)로 문자 데이터 "ABC"를 보유할 수 있습니다. 바이트의 데이터 길이가 3, 여부는 문자열 또는 문자 배열의로 처리 됩니다.  
  
 응용 프로그램 및 드라이버를 자주 사용 C 문자열 (null로 끝나는 배열 문자) 문자 데이터를 저장할 수 있지만이 작업을 수행 하는 요구 사항이 있습니다. C에서는 문자 데이터 문자 (null 종료)의 배열 및 길이/표시기 버퍼에 개별적으로 전달 된 바이트 길이으로 처리할 수도 있습니다.  
  
 문자 데이터는 비-null로 끝나는 배열에 저장할 수 있고를 해당 바이트 길이 개별적으로 전달 되므로 문자 데이터에 null 문자를 포함할 수 있습니다. 그러나 ODBC 함수의 동작은 경우 정의 되지 않습니다 이므로 드라이버 관련 여부 드라이버를 정확 하 게 처리이 있습니다. 따라서 상호 운용 가능한 응용 프로그램 이진 데이터가 포함 된 null 문자를 포함할 수 있는 문자 데이터를 항상 처리 해야 합니다.
