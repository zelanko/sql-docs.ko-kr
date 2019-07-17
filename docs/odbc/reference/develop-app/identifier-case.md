---
title: 식별자 대/소문자 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 70728908f081ab89e08cad1265f04394f29b66ef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138970"
---
# <a name="identifier-case"></a>식별자 사례
SQL 문 및 카탈로그 함수 인수 식별자와 따옴표 붙은 식별자 일 수 있습니다 대/소문자 구분 또는 그렇지 않은 응용 프로그램 호출 하 여 확인할 수 있는 **SQLGetInfo** SQL_QUOTED_ SQL_IDENTIFIER_CASE와 IDENTIFIER_CASE 옵션입니다.  
  
 이러한 각 옵션에 네 가지 가능한 반환 값: 하나의 않다는 식별자 또는 따옴표 붙은 식별자 대/소문자를 구분 하 고 세 가지 중요 하지 않다는 내용의 합니다. 대/소문자 구분 되지 않은 세 개의 값 추가 식별자 시스템 카탈로그에 저장 되는 사례를 설명 합니다. 응용 프로그램 카탈로그 함수의 결과 표시 하는 경우와 같은 표시를 위해 관련 된 식별자가 시스템 카탈로그에 저장 되는 방법 식별자의 대/소문자 구분은 변경 되지 않습니다.
