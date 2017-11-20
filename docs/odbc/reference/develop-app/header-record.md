---
title: "헤더 레코드 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- header records [ODBC]
- diagnostic records [ODBC]
ms.assetid: d0fff1ed-5616-422a-a394-7ea1d2486f89
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0e4b73bf94c2d90f34c1d06240cbcceb07702c7a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="header-record"></a>헤더 레코드
헤더 레코드의 필드는 반환 코드, 행 개수, 상태 레코드의 수 및 실행 된 문 유형 등 함수 실행에 대 한 일반 정보를 포함 합니다. 헤더 레코드는 함수에서 SQL_INVALID_HANDLE을 반환 하지 않는 한 항상 만들어집니다. 헤더 레코드의 필드 목록은 전체 참조는 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) 함수 설명 합니다.

