---
title: 식별자 Case | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138970"
---
# <a name="identifier-case"></a>식별자 사례
SQL 문 및 카탈로그 함수 인수에서 식별자와 따옴표 붙은 식별자는 대/소문자를 구분 하거나 사용 하지 않을 수 있습니다 .이 경우 응용 프로그램은 SQL_IDENTIFIER_CASE 및 SQL_QUOTED_IDENTIFIER_CASE 옵션으로 **SQLGetInfo** 를 호출 하 여 확인할 수 있습니다.  
  
 이러한 각 옵션에는 네 개의 가능한 반환 값이 있습니다. 하나는 식별자 또는 따옴표 붙은 식별자의 대/소문자가 중요 하다는 것을 나타내는 것입니다. 대/소문자를 구분 하지 않는 세 가지 값은 식별자가 시스템 카탈로그에 저장 되는 경우를 설명 합니다. 식별자가 시스템 카탈로그에 저장 되는 방법은 표시 목적 으로만 사용 됩니다. 예를 들어 응용 프로그램에서 카탈로그 함수의 결과를 표시 하는 경우에만 해당 됩니다. 식별자의 대/소문자 구분을 변경 하지 않습니다.
