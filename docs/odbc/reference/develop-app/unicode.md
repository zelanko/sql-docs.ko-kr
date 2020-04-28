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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9824e76cebabb6f5f84505292801a0094e359f0f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302449"
---
# <a name="unicode"></a>유니코드(Unicode)
유니코드는 여러 언어의 문자에 대 한 인코딩을 정의 합니다.  
  
 유니코드 표준에 대 한 자세한 내용은 [Unicode Consortium](https://www.unicode.org)을 참조 하십시오.  
  
 유니코드는 유니버설 문자 집합을 정의 합니다. Windows ANSI 코드 페이지는 문자 집합을 정의 합니다. 문자 집합은 일반적으로 한 언어에 대 한 문자를 포함 합니다. 다른 코드 페이지를 사용 하는 데 필요한 응용 프로그램을 작성 하는 것이 더 어려울 수 있습니다.  
  
 유니코드에는 코드 페이지가 필요 하지 않습니다. 모든 코드 포인트는 일부 언어의 단일 문자에 매핑됩니다.  
  
 현재 ODBC에서 지 원하는 유일한 유니코드 인코딩은 u s-2 이며,이는 16 비트 정수 (고정 길이)를 사용 하 여 문자를 나타냅니다. 유니코드를 사용 하면 응용 프로그램이 다른 언어로 작동할 수 있습니다.  
  
 ODBC 3.5 이상 드라이버 관리자는 유니코드를 사용할 수 있습니다. 이는 함수 호출 및 문자열 데이터 형식과 같은 두 가지 주요 영역에 영향을 줍니다. 드라이버 관리자는 응용 프로그램 및 드라이버에서 요구 하는 함수 문자열 인수 및 문자열 데이터를 매핑합니다. 둘 다 유니코드를 사용 하도록 설정 하거나 ANSI를 사용할 수 있습니다. 이러한 두 영역에 대해서는 [유니코드 함수 인수](../../../odbc/reference/develop-app/unicode-function-arguments.md) 및 [유니코드 데이터](../../../odbc/reference/develop-app/unicode-data.md)섹션에서 자세히 설명 합니다.  
  
 ODBC 3.5 이상 드라이버 관리자는 유니코드 응용 프로그램과 ANSI 응용 프로그램 모두에서 유니코드 드라이버를 사용할 수 있도록 지원 합니다. Ansi 응용 프로그램에 ANSI 드라이버를 사용 하는 것도 지원 합니다. 드라이버 관리자는 ANSI 드라이버를 사용 하는 유니코드 응용 프로그램에 대해 제한 된 유니코드-ANSI 매핑을 제공 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [유니코드 함수 인수](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [유니코드 데이터](../../../odbc/reference/develop-app/unicode-data.md)
