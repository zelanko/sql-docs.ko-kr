---
title: 식별자 케이스 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- identifiers [ODBC], case
- interoperability of SQL statements [ODBC], identifier case
ms.assetid: ee8a31aa-389d-4dd1-bfa9-547f6b50bc70
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 940d96ece6b2c344fa02e0daadd6248270f4d19e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300153"
---
# <a name="identifier-case"></a>식별자 사례
SQL 문 및 카탈로그 함수 인수에서 식별자와 quoted식별자는 대/소문자를 구분할 수 있으며, 응용 프로그램은 SQL_IDENTIFIER_CASE 및 SQL_QUOTED_IDENTIFIER_CASE 옵션으로 **SQLGetInfo를** 호출하여 결정할 수 있습니다.  
  
 이러한 옵션 각각에는 식별자 또는 인용 식별자 대/소문자가 민감하다는 내용과 민감하지 않다는 세 가지의 반환 값이 있습니다. 대/소문자를 구분하지 않는 세 가지 값은 식별자가 시스템 카탈로그에 저장되는 경우를 더 자세히 설명합니다. 식별자가 시스템 카탈로그에 저장되는 방식은 응용 프로그램이 카탈로그 함수의 결과를 표시하는 경우와 같이 표시 용도로만 관련이 있습니다. 식별자의 대/소문자를 변경하지 않습니다.
