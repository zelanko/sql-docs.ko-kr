---
title: "동시성 모델 (Visual FoxPro ODBC 드라이버)를 지원 합니다. | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], concurrency
- concurrency models [ODBC]
- FoxPro ODBC driver [ODBC], concurrency
ms.assetid: c39ed963-3af1-4888-8631-6083692ddcd7
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 769c6efaf95b1642209fa46b292822914261b826
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>지원 되는 동시성 모델 (Visual FoxPro ODBC 드라이버)
Visual FoxPro ODBC 드라이버가 지 원하는 *읽기 전용 동시성*합니다. 응용 프로그램에서 호출할 수 [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) SQL_CONCUR_READ_ONLY의 SQL_CONCURRENCY 옵션을 사용 합니다.  
  
 자세한 내용은 참조는 [ODBC Programmer's Reference](../../odbc/reference/odbc-programmer-s-reference.md)합니다.  
  
## <a name="read-only-concurrency"></a>읽기 전용 동시성  
 커서를 업데이트할 수 없습니다.  
  
## <a name="row-versioning"></a>행 버전 관리(row versioning)  
 기본적으로 타임 스탬프 지원, 행 버전이 업데이트 시 비교 됩니다.
