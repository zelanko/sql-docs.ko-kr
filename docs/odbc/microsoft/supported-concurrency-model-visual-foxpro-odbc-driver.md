---
title: 지원되는 동시성 모델(비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], concurrency
- concurrency models [ODBC]
- FoxPro ODBC driver [ODBC], concurrency
ms.assetid: c39ed963-3af1-4888-8631-6083692ddcd7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 253a6dd86f6dc974d53dd151636bb8b8132e4d02
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307719"
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>지원되는 동시성 모델(Visual FoxPro ODBC 드라이버)
Visual FoxPro ODBC 드라이버는 *읽기 전용 동시성을*지원합니다. 응용 프로그램은 SQL_CONCURRENCY SQL_CONCUR_READ_ONLY 옵션으로 [SQLSetStmtOption을](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) 호출할 수 있습니다.  
  
 자세한 내용은 [ODBC 프로그래머의 참조를](../../odbc/reference/odbc-programmer-s-reference.md)참조하십시오.  
  
## <a name="read-only-concurrency"></a>읽기 전용 동시성  
 커서를 업데이트할 수 없습니다.  
  
## <a name="row-versioning"></a>행 버전 관리(row versioning)  
 기본적으로 타임스탬프는 업데이트 시 행 버전을 비교하는 지원입니다.
