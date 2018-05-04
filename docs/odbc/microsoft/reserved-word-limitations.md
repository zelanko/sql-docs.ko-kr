---
title: Word 제한 사항 예약 | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ed42f083-c9e8-4ee4-9d64-d879bf955c78
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 010546fe5d0d987443fb4deebc4409cb5e867085
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="reserved-keyword-limitations"></a>예약 된 키워드 제한 사항

SQL 테이블 또는 관련된 개체에서 식별자로 ODBC 예약 된 키워드를 사용 하지 마십시오. 홀수 경우 예약된 된 키워드를 식별자로 사용 해야 경우, 식별자의 쌍으로 둘러싸야 *backticks* ('). 에 다른 이름을 *억음 악센트 기호* 은 *억음 악센트*합니다.

예약 된 키워드 제한의 예약 된 키워드의 약식 부분도에 적용 됩니다.

ODBC 예약 된 키워드 목록은에서 찾을 수 있습니다:

- [ODBC 예약 된 키워드](https://docs.microsoft.com/sql/odbc/reference/appendixes/reserved-keywords)합니다.

- 에 *ODBC 프로그래머 참조 가이드*, 참조 [부록 c: SQL 문법을](https://docs.microsoft.com/sql/odbc/reference/appendixes/appendix-c-sql-grammar)합니다.

