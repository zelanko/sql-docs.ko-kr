---
title: 유니코드 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1e6201b83b909573476b043cdb1a10543f894def
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51661812"
---
# <a name="unicode"></a>유니코드
유니코드는 많은 언어의 문자 인코딩을 정의 합니다.  
  
 유니코드 표준에 대 한 자세한 내용은 참조 하세요. [유니코드 컨소시엄](https://www.unicode.org)합니다.  
  
 유니코드 유니버설 문자 집합을 정의합니다. Windows ANSI 코드 페이지에는 일반적으로 하나의 언어에 대 한 문자가 포함 된 문자 집합을 정의 합니다. 다른 코드 페이지를 사용 하는 데 필요한 응용 프로그램을 작성 하는 것이 어려울 수 있습니다.  
  
 유니코드 코드 페이지를 필요 하지 않습니다. 모든 코드 포인트는 일부 언어에서 단일 문자에 매핑됩니다.  
  
 현재 유일한 유니코드 ODBC 지 인코딩 문자를 표현 하는 16 비트 정수 (고정된 길이)를 사용 하는 ucs-2입니다. 유니코드에는 다른 언어에서 작동 하도록 응용 프로그램이 있습니다.  
  
 ODBC 3.5 (또는 이상) 드라이버 관리자는 유니코드를 지원 합니다. 이 두 가지 주요 영역에 영향을 줍니다: 함수 호출 및 문자열 데이터 형식입니다. 드라이버 관리자 맵 함수 문자열 인수 및 응용 프로그램 및 드라이버에서 필요에 따라 문자열 데이터를 유니코드를 지원 또는 ANSI 설정 둘 다이 가능 합니다. 이러한 두 영역 섹션에 대 한 자세한 설명은 [유니코드 함수 인수](../../../odbc/reference/develop-app/unicode-function-arguments.md) 하 고 [유니코드 데이터](../../../odbc/reference/develop-app/unicode-data.md)입니다.  
  
 ODBC 3.5 (또는 이상) 드라이버 관리자는 응용 프로그램을 유니코드 및 ANSI 응용 프로그램을 사용 하 여 유니코드 드라이버의 사용을 지원합니다. 또한 ANSI 응용 프로그램을 사용 하 여 ANSI 드라이버를 사용을 지원합니다. 드라이버 관리자는 ANSI 드라이버를 사용 하는 유니코드 응용 프로그램에 대 한 제한 된 유니코드에서 ANSI로 매핑을 제공 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [유니코드 함수 인수](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [유니코드 데이터](../../../odbc/reference/develop-app/unicode-data.md)
