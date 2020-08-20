---
description: 문자 데이터 및 C 문자열
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e412976cb297af9a9e38bbc6991647eeab48483b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465925"
---
# <a name="character-data-and-c-strings"></a>문자 데이터 및 C 문자열
가변 길이 문자 데이터를 참조 하는 입력 매개 변수 (예: 열 이름, 동적 매개 변수 및 문자열 특성 값)에는 연결 된 길이 매개 변수가 있습니다. 응용 프로그램이 C에서와 같이 null 문자를 사용 하 여 문자열을 종료 하는 경우 문자열의 길이 (null 종결자를 포함 하지 않음) 또는 SQL_NTS (Null로 끝나는 문자열)의 길이를 인수로 제공 합니다. 음수 길이가 아닌 인수는 연결 된 문자열의 실제 길이를 지정 합니다. 길이가 0 인 문자열을 지정 하려면 길이 인수가 0 일 수 있으며,이는 NULL 값과 구분 됩니다. 음수 값 SQL_NTS null 종료 문자를 찾아 드라이버에 문자열 길이를 결정 하도록 지시 합니다.  
  
 드라이버에서 응용 프로그램으로 문자 데이터가 반환 되는 경우 드라이버는 항상 null로 종료 되어야 합니다. 이를 통해 응용 프로그램에서 데이터를 문자열 또는 문자 배열로 처리할지 여부를 선택할 수 있습니다. 응용 프로그램 버퍼가 작아서 문자 데이터를 모두 반환 하기에 충분 하지 않은 경우 드라이버는 버퍼의 바이트 길이로 null 종료 문자에 필요한 바이트 수를 뺀 값을 자릅니다 .는 잘린 데이터를 null로 종료 하 고 버퍼에 저장 합니다. 따라서 응용 프로그램은 문자 데이터를 검색 하는 데 사용 되는 버퍼의 null 종료 문자에 대해 항상 추가 공간을 할당 해야 합니다. 예를 들어 51 바이트 버퍼는 50 문자 데이터를 검색 하는 데 필요 합니다.  
  
 **Sqlputdata** 또는 **SQLGetData**를 사용 하는 부분에서 긴 문자 데이터를 전송 하거나 검색할 때 응용 프로그램과 드라이버 모두에서 특별히 주의를 기울여야 합니다. 데이터가 일련의 null로 끝나는 문자열로 전달 되는 경우 데이터를 리 어셈블 하려면 이러한 문자열의 null 종결 문자를 제거 해야 합니다.  
  
 많은 ODBC 프로그래머는 문자 데이터와 C 문자열이 혼동 됩니다. 이는 ODBC 함수를 정의할 때 C 언어를 사용 하는 아티팩트입니다. ODBC 드라이버 또는 응용 프로그램에서 다른 언어를 사용 하는 경우-ODBC는 언어 독립적 이므로 이러한 혼란이 발생할 가능성은 낮습니다.  
  
 C 문자열이 문자 데이터를 저장 하는 데 사용 되는 경우 null 종료 문자는 데이터의 일부로 간주 되지 않으며 바이트 길이의 일부로 계산 되지 않습니다. 예를 들어 문자 데이터 "ABC"는 C 문자열 "ABC\0" 또는 문자 배열 {' A ', ' B ', ' C '}로 저장할 수 있습니다. 데이터의 바이트 길이는 문자열 또는 문자 배열로 처리 되는지 여부에 상관 없이 3입니다.  
  
 응용 프로그램 및 드라이버는 일반적으로 C 문자열 (null로 끝나는 문자 배열)을 사용 하 여 문자 데이터를 저장 하지만이 작업을 수행 하기 위한 요구 사항은 없습니다. C에서 문자 데이터는 문자 배열 (null 종결 없음) 및 바이트 길이가 길이/표시기 버퍼에서 별도로 전달 될 수도 있습니다.  
  
 문자 데이터는 null로 끝나는 배열 및 해당 바이트 길이에 개별적으로 전달 될 수 있으므로 문자 데이터에 null 문자를 포함할 수 있습니다. 그러나이 경우에는 ODBC 함수의 동작이 정의 되어 있지 않으며 드라이버가이를 올바르게 처리 하는지 여부는 드라이버 별로 다릅니다. 따라서 상호 운용 가능한 응용 프로그램은 항상 포함 된 null 문자를 이진 데이터로 포함할 수 있는 문자 데이터를 처리 해야 합니다.
