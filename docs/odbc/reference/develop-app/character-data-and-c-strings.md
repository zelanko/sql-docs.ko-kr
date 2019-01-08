---
title: 문자 데이터 및 C 문자열 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 00daac655f0c435c1ee22239d3d4aafa23065997
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52515887"
---
# <a name="character-data-and-c-strings"></a>문자 데이터 및 C 문자열
가변 길이 문자 데이터 (예: 열 이름, 동적 매개 변수 및 문자열 특성 값)를 참조 하는 입력된 매개 변수는 연결 된 길이 매개 변수를 갖습니다. 응용 프로그램이 종료 null 문자는 C에서 일반적으로 사용 하 여 문자열, 바이트 문자열 (null 종결자를 제외)의 길이 또는 SQL_NTS (Null-Terminated 문자열)를 인수로 제공 합니다. 음수가 아닌 길이 인수를 연결 된 문자열의 실제 길이 지정합니다. 길이 인수는 NULL 값을 길이가 0 인 문자열을 지정 하려면 0을 수 있습니다. SQL_NTS 음수 값을 null 종료 문자를 배치 하 여 문자열의 길이 확인 하는 드라이버를 전달 합니다.  
  
 문자 데이터는 응용 프로그램에는 드라이버에서 반환 되 면 드라이버 해야 항상 null로 종료 것입니다. 이렇게 하면 응용 프로그램을 문자열 또는 문자 배열로 데이터를 처리할지 여부를 선택 합니다. 응용 프로그램 버퍼를 충분히 모든 문자 데이터를 반환할 수 없는 경우 드라이버는 null 종결 문자에 따라 필요한 바이트 수를 뺀 버퍼의 바이트 길이, 잘린된 데이터를 null로 끝냅니다 잘리고에 저장 합니다 버퍼입니다. 따라서 응용 프로그램 문자 데이터를 검색 하는 데 사용 되는 버퍼에 null 종료 문자에 대 한 추가 공간이 할당 항상 해야 합니다. 예를 들어 51 바이트 버퍼를 50 개 문자 데이터를 검색할 필요 합니다.  
  
 응용 프로그램과 보내거나 사용 하 여 파트의 긴 문자 데이터를 검색 하는 경우 드라이버에서 특별 한 주의 기울여 수 **SQLPutData** 하거나 **SQLGetData**합니다. 데이터를 일련의 null로 끝나는 문자열을 전달 하면 데이터를 어셈블해야 수 전에 이러한 문자열에 null 종료 문자를 제거 해야 합니다.  
  
 ODBC 프로그래머의 숫자로 있는 문자 데이터 및 C 문자열 혼동 됩니다. ODBC 함수를 정의 하는 경우에 C 언어를 사용 하 여 아티팩트는이 발생 했습니다. ODBC 드라이버 또는 응용 프로그램에서 다른 언어-를 사용 하는 경우에 ODBC는 언어 독립적-이러한 혼동이 발생할 가능성은 해야 합니다.  
  
 C 문자열을 사용 하 여 문자 데이터를 보관, null 종료 문자 데이터의 일부로 간주 되지 않습니다 및 바이트 길이의 일부로 계산 되지 않습니다. 예를 들어, 문자 데이터 "ABC"는 "ABC\0" C 문자열 또는 문자 배열 {'A', 'B', 'C'을 (를) 보관할 수 있습니다. 데이터의 바이트 길이 3, 문자열 또는 문자 배열로 처리 됩니다 여부입니다.  
  
 응용 프로그램 및 드라이버 일반적으로 사용 하 여 있지만 C 문자열 (null로 끝나는 배열 문자) 문자 데이터를 저장,이 작업을 수행 하는 요구 사항이 있습니다. C에서 문자 데이터 (null 종료)에 없는 문자 배열 길이/표시기 버퍼에 따로 전달 바이트 길이와 처리할 수도 있습니다.  
  
 Null로 끝나지 않는 배열에 문자 데이터를 보관할 수 있습니다 하 고 해당 바이트 길이 개별적으로 전달 되므로 문자 데이터에서 null 문자를 포함할 수 있습니다. 그러나 ODBC 함수의 동작은 경우 정의 되지 이므로 드라이버별 여부 드라이버가이 올바르게 처리 합니다. 따라서 상호 운용 가능한 응용 프로그램 이진 데이터가 포함 된 null 문자를 포함할 수 있는 문자 데이터를 항상 처리 해야 합니다.
