---
title: 예약어 제한 사항 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c884d8594c3c4511bed0e24f9b3dd43092176b4e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67988021"
---
# <a name="reserved-keyword-limitations"></a>예약 키워드 제한 사항

SQL 테이블 또는 관련 개체에서 ODBC 예약 키워드를 식별자로 사용 하지 마십시오. 이름으로 예약 된 키워드를 사용 해야 하는 경우를 대비 하 여 식별자를 *backtick* (') 쌍으로 묶어야 합니다. *억음* 의 또 다른 이름은 *back 따옴표*입니다.

예약 키워드 제한은 예약 된 키워드의 모든 줄임 형식에도 적용 됩니다.

ODBC 예약 키워드 목록은 다음 위치에서 제공 됩니다.

- [ODBC 예약 키워드](https://docs.microsoft.com/sql/odbc/reference/appendixes/reserved-keywords)입니다.

- *ODBC 프로그래머 참조 가이드*에서 [부록 C: SQL 문법](https://docs.microsoft.com/sql/odbc/reference/appendixes/appendix-c-sql-grammar)을 참조 하세요.

