---
title: 헤더 레코드 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- header records [ODBC]
- diagnostic records [ODBC]
ms.assetid: d0fff1ed-5616-422a-a394-7ea1d2486f89
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 372185966cc1644147feb2683177ae3a5b69e788
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300183"
---
# <a name="header-record"></a>헤더 레코드
헤더 레코드의 필드에는 반환 코드, 행 수, 상태 레코드 수 및 실행된 명령문 유형을 비롯하여 함수의 실행에 대한 일반 정보가 포함됩니다. 함수가 SQL_INVALID_HANDLE 반환하지 않는 한 헤더 레코드는 항상 만들어집니다. 헤더 레코드의 전체 필드 목록은 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) 함수 설명을 참조하십시오.
