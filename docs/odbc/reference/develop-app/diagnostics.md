---
title: 진단 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC]
- functions [ODBC], diagnostic information
- diagnostic information [ODBC], about diagnostic information
ms.assetid: 450abd88-90a1-4fbc-b417-8efbdd8e1dea
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b6ffbcdac7a478f8edd6560610811ddff6952b0d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="diagnostics"></a>진단
Odbc에서 함수는 두 가지 방법으로 진단 정보를 반환합니다. 반환 코드 진단 레코드는 함수에 대 한 자세한 정보를 제공 하는 동안 전반적인 성공 또는 실패는 함수를 나타냅니다. 하나 이상의 진단 레코드-헤더 레코드-함수가 성공 하는 경우에 반환 됩니다.  
  
 진단 정보는 하드 코드 된 SQL 문에서 잘못 된 핸들이 같은 프로그래밍 오류와 구문 오류를 catch 하려면 개발 시에 사용 됩니다. 런타임 오류 및 경고 데이터 잘림, 액세스 위반 및 구문 오류와 같은 사용자가 입력 한 SQL 문에서 catch를 런타임에 사용 됩니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [반환 코드](../../../odbc/reference/develop-app/return-codes-odbc.md)  
  
-   [진단 레코드](../../../odbc/reference/develop-app/diagnostic-records.md)  
  
-   [SQLGetDiagRec 및 SQLGetDiagField 사용](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [SQLGetDiagRec 및 SQLGetDiagField 구현](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [진단 처리 예제](../../../odbc/reference/develop-app/diagnostic-handling-examples.md)
