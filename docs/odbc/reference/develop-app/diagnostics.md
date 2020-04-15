---
title: 진단 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC]
- functions [ODBC], diagnostic information
- diagnostic information [ODBC], about diagnostic information
ms.assetid: 450abd88-90a1-4fbc-b417-8efbdd8e1dea
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a09f46d3fd6aa2f9b9c7310af6d3ddc90f78389f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305154"
---
# <a name="diagnostics"></a>진단
ODBC의 함수는 두 가지 방법으로 진단 정보를 반환합니다. 반환 코드는 함수의 전반적인 성공 또는 실패를 나타내며 진단 레코드는 함수에 대한 자세한 정보를 제공합니다. 함수가 성공하더라도 하나 이상의 진단 레코드(헤더 레코드)가 반환됩니다.  
  
 진단 정보는 개발 시 하드 코딩된 SQL 문에서 잘못된 핸들 및 구문 오류와 같은 프로그래밍 오류를 catch하는 데 사용됩니다. 런타임에 데이터 잘림, 액세스 위반 및 사용자가 입력한 SQL 문의 구문 오류와 같은 런타임 오류 및 경고를 catch하는 데 사용됩니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [반환 코드](../../../odbc/reference/develop-app/return-codes-odbc.md)  
  
-   [진단 레코드](../../../odbc/reference/develop-app/diagnostic-records.md)  
  
-   [SQLGetDiagRec 및 SQLGetDiagField 사용](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [SQLGetDiagRec 및 SQLGetDiagField 구현](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [진단 처리 예제](../../../odbc/reference/develop-app/diagnostic-handling-examples.md)
