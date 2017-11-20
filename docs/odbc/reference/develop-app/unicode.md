---
title: "유니코드 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Unicode [ODBC]
- Unicode [ODBC], about Unicode
ms.assetid: 113e1c9a-8333-4805-86f2-e4b57ab816a5
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7ec40cc841c073fe66f9537687516f044048a0fc
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="unicode"></a>유니코드
유니코드 문자 여러 언어에 대 한 인코딩을 정의 합니다.  
  
 유니코드 표준에 대 한 자세한 내용은 참조 [The 유니코드 컨소시엄](http://www.unicode.org)합니다.  
  
 유니코드 유니버설 문자 집합을 정의합니다. Windows ANSI 코드 페이지는 일반적으로 한 언어에 대 한 문자를 포함 하는 문자 집합을 정의 합니다. 서로 다른 코드 페이지를 사용 하는 데 필요한 응용 프로그램을 작성 하기 어려울 수 있습니다.  
  
 유니코드는 코드 페이지를 필요 하지 않습니다. 모든 코드 포인트는 일부 언어에서 단일 문자에 매핑됩니다.  
  
 현재 유일한 유니코드 ODBC 지 원하는 인코딩을 u c S 2를 사용 하는 16 비트 정수 (고정된 길이) 나타내는 문자입니다. 유니코드를 사용 하면 서로 다른 언어에서 작동 하도록 응용 프로그램.  
  
 ODBC 3.5 (또는 이상) 드라이버 관리자는 유니코드를 지원 합니다. 두 가지 주요 영역을 미치면: 함수 호출 하 고 문자열 데이터 형식입니다. 드라이버 관리자 지도 함수 문자열 인수 및 응용 프로그램 및 드라이버에서 필요에 따라 문자열 데이터를 유니코드 사용 가능 또는 ANSI 설정 중 하나는 모두 일 수 있습니다. 이러한 두 영역 섹션에서 자세히 설명 [유니코드 함수 인수](../../../odbc/reference/develop-app/unicode-function-arguments.md) 및 [유니코드 데이터](../../../odbc/reference/develop-app/unicode-data.md)합니다.  
  
 ODBC 3.5 (또는 이상) 드라이버 관리자 유니코드 응용 프로그램 및 ANSI 응용 프로그램이 모두와 유니코드 드라이버의 사용을 지원 합니다. 또한 ANSI 응용 프로그램으로 ANSI 드라이버의 사용을 지원 합니다. 드라이버 관리자 ANSI 드라이버를 사용 하는 유니코드 응용 프로그램에 대 한 제한 된 유니코드에서 ANSI 매핑을 제공 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [유니코드 함수 인수](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [유니코드 데이터](../../../odbc/reference/develop-app/unicode-data.md)

