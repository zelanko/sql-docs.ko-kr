---
description: 지원되는 동시성 모델(Visual FoxPro ODBC 드라이버)
title: 지원 되는 동시성 모델 (Visual FoxPro ODBC 드라이버) | Microsoft Docs
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
ms.openlocfilehash: 1be0a7e9ea3700941282f23956a8c304a1ef7f5e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500106"
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>지원되는 동시성 모델(Visual FoxPro ODBC 드라이버)
Visual FoxPro ODBC 드라이버는 *읽기 전용 동시성*을 지원 합니다. 응용 프로그램은 SQL_CONCURRENCY 옵션 SQL_CONCUR_READ_ONLY를 사용 하 여 [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) 를 호출할 수 있습니다.  
  
 자세한 내용은 [ODBC 프로그래머 참조](../../odbc/reference/odbc-programmer-s-reference.md)를 참조 하세요.  
  
## <a name="read-only-concurrency"></a>읽기 전용 동시성  
 커서를 업데이트할 수 없습니다.  
  
## <a name="row-versioning"></a>행 버전 관리(row versioning)  
 기본적으로 타임 스탬프 지원은 업데이트 시 행 버전을 비교 합니다.
