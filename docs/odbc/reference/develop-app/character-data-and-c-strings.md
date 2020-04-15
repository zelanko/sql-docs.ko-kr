---
title: 문자 데이터 및 C 문자열 | 마이크로 소프트 문서
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
ms.openlocfilehash: 7bb25022d4e0c0559f2a8f77b89a4ba26aeba33a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307493"
---
# <a name="character-data-and-c-strings"></a>문자 데이터 및 C 문자열
가변 길이 문자 데이터(예: 열 이름, 동적 매개 변수 및 문자열 특성 값)를 참조하는 입력 매개변수에는 연관된 길이 매개 변수가 있습니다. 응용 프로그램이 C에서 일반적인 것처럼 null 문자로 문자열을 종료하는 경우 문자열의 바이트 길이(null-terminator 포함)또는 SQL_NTS(Null-Terminated String)을 인수로 제공합니다. 음수가 아닌 길이 인수는 연결된 문자열의 실제 길이를 지정합니다. 길이 인수는 NULL 값과 구별되는 0길이 문자열을 지정하기 위해 0일 수 있습니다. 음수 값 SQL_NTS null 종료 문자를 찾아 문자열의 길이를 결정 하도록 드라이버를 지시 합니다.  
  
 드라이버에서 응용 프로그램으로 문자 데이터가 반환되는 경우 드라이버는 항상 null-terminate해야 합니다. 이렇게 하면 응용 프로그램에서 데이터를 문자열또는 문자 배열로 처리할지 여부를 선택할 수 있습니다. 응용 프로그램 버퍼가 모든 문자 데이터를 반환할 만큼 크지 않은 경우 드라이버는 null-termination 문자에 필요한 바이트 수를 적게 버퍼의 바이트 길이로 잘리고 잘린 데이터를 null-terminate및 버퍼에 저장합니다. 따라서 응용 프로그램은 항상 문자 데이터를 검색하는 데 사용되는 버퍼에서 null-termination 문자에 대한 추가 공간을 할당해야 합니다. 예를 들어 50자 의 데이터를 검색하려면 51바이트 버퍼가 필요합니다.  
  
 **SQLPutData** 또는 **SQLGetData를**사용하여 긴 문자 데이터를 일부에서 보내거나 검색할 때 응용 프로그램과 드라이버 모두 특별한주의를 기울여야합니다. 데이터가 일련의 null 종료 문자열로 전달되는 경우 데이터를 다시 어셈블하기 전에 이러한 문자열의 null 종료 문자를 제거해야 합니다.  
  
 많은 ODBC 프로그래머가 문자 데이터와 C 문자열을 혼동했습니다. 이 발생은 ODBC 함수를 정의할 때 C 언어를 사용하는 아티팩트입니다. ODBC 드라이버 또는 응용 프로그램이 다른 언어를 사용하는 경우 - ODBC는 언어독립적이라는 것을 기억하십시오 - 이 혼동이 발생할 가능성이 적습니다.  
  
 C 문자열이 문자 데이터를 보유하는 데 사용되는 경우 null-termination 문자는 데이터의 일부로 간주되지 않으며 바이트 길이의 일부로 계산되지 않습니다. 예를 들어 문자 데이터 "ABC"는 C 문자열 "ABC\0" 또는 문자 배열 {'A', 'B', 'C'}로 보유할 수 있습니다. 데이터의 바이트 길이는 문자열 또는 문자 배열로 처리되는지 여부에 관계없이 3입니다.  
  
 응용 프로그램과 드라이버는 일반적으로 문자 데이터를 보유하기 위해 C 문자열(null-terminated 문자 배열)을 사용하지만 이 작업을 수행할 필요는 없습니다. C에서 문자 데이터는 null 종료 없이 문자 배열로 처리될 수 있으며 길이/표시기 버퍼에서 해당 바이트 길이가 별도로 전달됩니다.  
  
 문자 데이터는 null이 아닌 종료 배열에 보관할 수 있고 바이트 길이가 별도로 전달되므로 문자 데이터에 null 문자를 포함할 수 있습니다. 그러나 이 경우 ODBC 함수의 동작은 정의되지 않으며 드라이버가 이 것을 올바르게 처리하는지 여부는 드라이버에 따라 다릅니다. 따라서 상호 운용 가능한 응용 프로그램은 항상 포함된 null 문자를 이진 데이터로 포함할 수 있는 문자 데이터를 처리해야 합니다.
