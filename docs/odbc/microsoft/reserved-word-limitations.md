---
title: 예약된 단어 제한 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 05/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ed42f083-c9e8-4ee4-9d64-d879bf955c78
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf536e06556e6b2e7b27f220d09a51f91b44d23c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304011"
---
# <a name="reserved-keyword-limitations"></a>예약된 키워드 제한 사항

ODBC 예약 키워드를 SQL 테이블 이나 관련 개체의 식별자로 사용하지 마십시오. 예약된 키워드를 식별자로 사용해야 하는 이상한 경우가 발생하는 경우 식별자를 *백틱(')* 쌍으로 둘러싸야 합니다. *backtick의* 또 다른 이름은 *다시 따옴표입니다.*

예약된 키워드 제한은 예약된 키워드의 모든 약어 형식에도 적용됩니다.

ODBC 예약 키워드 목록은 다음 에서 확인할 수 있습니다.

- [ODBC 예약 키워드](https://docs.microsoft.com/sql/odbc/reference/appendixes/reserved-keywords).

- *ODBC 프로그래머의 참조 가이드에서* [부록 C: SQL 문법](https://docs.microsoft.com/sql/odbc/reference/appendixes/appendix-c-sql-grammar)을 참조하십시오.

