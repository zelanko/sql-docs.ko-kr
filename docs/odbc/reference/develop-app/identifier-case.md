---
title: 식별자 대/소문자 | Microsoft Docs
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
- SQL statements [ODBC], interoperability
- identifiers [ODBC], case
- interoperability of SQL statements [ODBC], identifier case
ms.assetid: ee8a31aa-389d-4dd1-bfa9-547f6b50bc70
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66218fb955a4133a5c689f72ab8f4b96504c9bd2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32908855"
---
# <a name="identifier-case"></a>식별자 대/소문자
SQL 문 및 카탈로그 함수 인수 식별자와 따옴표 붙은 식별자 일 수 대/소문자 구분 또는 응용 프로그램이 호출 하 여 확인할 수 있는, **SQLGetInfo** SQL_IDENTIFIER_CASE 및 SQL_QUOTED_ IDENTIFIER_CASE 옵션입니다.  
  
 이러한 각 옵션의 4 가지 가능한 반환 값: 하나의 식별자 또는 따옴표 붙은 식별자의 대/소문자가 구분 되 고 중요 하지 않다는 내용의 세 가지입니다. 대/소문자 구분 없는 3 개의 값 추가 식별자 시스템 카탈로그에 저장 되는 사례를 설명 합니다. 식별자가 시스템 카탈로그에 저장 되는 방법에 관련 된 응용 프로그램 카탈로그 함수의 결과 표시 하는 경우와 같은 내용을 표시 식별자의 대/소문자 구분은 변경 되지 않습니다.
