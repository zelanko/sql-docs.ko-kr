---
title: S Q l-92 호환성 | Microsoft Docs
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
- Jet-based ODBC drivers [ODBC], SQL-92 compliance
- desktop database drivers [ODBC], SQL-92 compliance
- SQL-92 compliance [ODBC]
- ODBC desktop database drivers [ODBC], SQL-92 compliance
ms.assetid: 50c8c7df-df01-4f4d-ad62-d059cf29d73a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 09b1a044a362207b5bc1c04d3a90e210ad7c8137
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sql-92-compliance"></a>S Q l-92 호환성
ODBC 데스크톱 데이터베이스 드라이버 및 기본 Microsoft Jet 엔진이 sql-92 호환 되지 않습니다. S Q l-92에 정의 된 많은 기능을 지원 합니다. 드라이버에서 지원 되는 일부 기능에 SQL 92 지원 되지 않습니다. 자세한 내용은 참조는 *Microsoft Jet 데이터베이스 엔진 Programmer's Guide*합니다. 다음은 두 항목 간의 주요 차이점입니다.  
  
-   데스크톱 데이터베이스 드라이버에서 사용 하는 SQL SQL 92 하 여 지정 된 것 보다 더 강력한 식을 지원 합니다.  
  
-   다양 한 규칙 BETWEEN 조건자에 적용 됩니다.  
  
-   데스크톱 데이터베이스 드라이버와 ANSI SQL에서 사용 하는 SQL 서로 다른 키워드를 지원 합니다.  
  
 다음과 같은 SQL 92 기능 Microsoft Jet SQL에서 지원 되지 않습니다.  
  
-   GRANT 및 잠금 같은 보안 문  
  
-   집계 함수 참조와 고유 값입니다.  
  
 다음 기능은 sql-92가 지정 되지 않은 데스크톱 데이터베이스 드라이버에서 사용 하는 SQL의 향상 된 기능을 보여 줍니다.  
  
-   크로스탭 쿼리에 대 한 지원을 제공 하는 변환 문입니다.  
  
-   집계 함수를 추가로 (**StDev** 및 **VarP**).  
  
> [!NOTE]  
>  데스크톱 데이터베이스 드라이버를 지 원하는 표준 ANSI 구문을 _ (밑줄) 및 백분율 (%)에 대 한 하지 * (별표) 하 고 있습니까? (물음표)입니다.
