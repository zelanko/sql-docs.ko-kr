---
title: 테이블 명세서 만들기에서 NULL이 아님 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- not null [ODBC]
- interoperability [ODBC], not null
ms.assetid: 3fb69943-f0c9-4ed2-aa42-20440e37e49d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 490f4a7e49acdad5f919ad21f93d479b03099eb4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302391"
---
# <a name="not-null-in-create-table-statements"></a>CREATE TABLE 문의 NOT NULL
일부 데이터베이스, 특히 데스크톱 데이터베이스는 **CREATE TABLE** 문에서 **NOT NULL** 열 제약 조건을 지원하지 않습니다. 자세한 내용은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명에서 SQL_NON_NULLABLE_COLUMNS 옵션을 참조하십시오.
