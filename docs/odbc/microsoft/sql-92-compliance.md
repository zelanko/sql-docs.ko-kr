---
title: SQL-92 컴플라이언스 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], SQL-92 compliance
- desktop database drivers [ODBC], SQL-92 compliance
- SQL-92 compliance [ODBC]
- ODBC desktop database drivers [ODBC], SQL-92 compliance
ms.assetid: 50c8c7df-df01-4f4d-ad62-d059cf29d73a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9ac0ae5873e545afb8fcac9dd003c984b1ed303a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300703"
---
# <a name="sql-92-compliance"></a>SQL-92 호환성
ODBC 데스크톱 데이터베이스 드라이버와 기본 Microsoft Jet 엔진은 SQL-92를 준수하지 않습니다. SQL-92에 정의된 많은 기능을 지원합니다. 드라이버에서 지원되는 일부 기능은 SQL-92에서 지원되지 않습니다. 자세한 내용은 Microsoft *Jet 데이터베이스 엔진 프로그래머 가이드를*참조하십시오. 다음은 두 가지 의 주요 차이점입니다.  
  
-   데스크톱 데이터베이스 드라이버에서 사용하는 SQL은 SQL-92에서 지정한 것보다 더 강력한 식을 지원합니다.  
  
-   BETWEEN 조건자에는 다른 규칙이 적용됩니다.  
  
-   데스크톱 데이터베이스 드라이버 및 ANSI SQL에서 사용하는 SQL은 서로 다른 키워드를 지원합니다.  
  
 다음 SQL-92 기능은 Microsoft Jet SQL에서 지원되지 않습니다.  
  
-   그랜트 및 잠금과 같은 보안 명령문.  
  
-   집계 함수 참조와 구별됩니다.  
  
 다음 기능은 SQL-92에서 지정하지 않은 데스크톱 데이터베이스 드라이버에서 사용하는 SQL의 향상된 기능입니다.  
  
-   크로스탭 쿼리에 대한 지원을 제공하는 TRANSFORM 문입니다.  
  
-   추가 집계**함수(StDev** 및 **VarP).**  
  
> [!NOTE]  
>  데스크톱 데이터베이스 드라이버는 표준 ANSI 구문을 %(퍼센트) 및 _(밑줄)에 대해 지원하지 않으며 * (별표) 및 ? 설정합니다.
