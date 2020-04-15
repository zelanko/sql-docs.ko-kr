---
title: 유니코드 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC]
- Unicode [ODBC], about Unicode
ms.assetid: 113e1c9a-8333-4805-86f2-e4b57ab816a5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9824e76cebabb6f5f84505292801a0094e359f0f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302449"
---
# <a name="unicode"></a>Unicode
유니코드는 여러 언어로 된 문자에 대한 인코딩을 정의합니다.  
  
 유니코드 표준에 대한 자세한 내용은 [유니코드 컨소시엄 을](https://www.unicode.org)참조하십시오.  
  
 유니코드는 범용 문자 집합을 정의합니다. Windows ANSI 코드 페이지는 일반적으로 한 언어에 대한 문자를 포함하는 문자 집합을 정의합니다. 다른 코드 페이지를 사용하는 데 필요한 응용 프로그램을 작성하는 것이 더 어려울 수 있습니다.  
  
 유니코드에는 코드 페이지가 필요하지 않습니다. 모든 코드 포인트는 일부 언어의 단일 문자에 매핑됩니다.  
  
 현재 ODBC가 지원하는 유일한 유니코드 인코딩은 문자를 나타내기 위해 16비트 정수(고정 길이)를 사용하는 UCS-2입니다. 유니코드를 사용하면 응용 프로그램이 다른 언어로 작동할 수 있습니다.  
  
 ODBC 3.5(그 이상) 드라이버 관리자는 유니코드가 활성화되어 있습니다. 이는 함수 호출과 문자열 데이터 형식의 두 가지 주요 영역에 영향을 줍니다. 드라이버 관리자는 응용 프로그램과 드라이버에서 요구하는 대로 함수 문자열 인수 및 문자열 데이터를 매핑하며, 둘 다 유니코드 지원 또는 ANSI 지원일 수 있습니다. 이 두 영역은 유니코드 함수 인수 및 [유니코드 데이터](../../../odbc/reference/develop-app/unicode-data.md)섹션에서 자세히 [설명합니다.](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
 ODBC 3.5(또는 그 이상) 드라이버 관리자는 유니코드 응용 프로그램과 ANSI 응용 프로그램을 모두 사용하는 유니코드 드라이버의 사용을 지원합니다. 또한 ANSI 응용 프로그램을 사용하여 ANSI 드라이버를 사용할 수 있습니다. 드라이버 관리자는 ANSI 드라이버로 작업하는 유니코드 응용 프로그램에 대해 제한된 유니코드-ANSI 매핑을 제공합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [유니코드 함수 인수](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [유니코드 데이터](../../../odbc/reference/develop-app/unicode-data.md)
