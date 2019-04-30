---
title: SQL-92 호환성 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf6d8d056c1658a924de4b108d3c0d025e8a58f1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63313399"
---
# <a name="sql-92-compliance"></a>SQL-92 호환성
ODBC 데스크톱 데이터베이스 드라이버 및 기본 Microsoft Jet 엔진이 SQL-92 호환 되지 않습니다. SQL-92에 정의 된 많은 기능을 지원 합니다. SQL-92에 드라이버에서 지원 되는 일부 기능을 사용할 수 없습니다. 자세한 내용은 참조는 *Microsoft Jet 데이터베이스 엔진 Programmer's Guide*합니다. 다음은 둘 사이의 주요 차이점:  
  
-   데스크톱 데이터베이스 드라이버를 사용한 SQL SQL-92 하 여 지정 된 것 보다 더 강력한 식을 지원 합니다.  
  
-   BETWEEN 조건자에 다른 규칙이 적용 됩니다.  
  
-   데스크톱 데이터베이스 드라이버와 ANSI SQL에서 사용 하는 SQL 다양 한 키워드를 지원 합니다.  
  
 SQL-92 기능인 Microsoft Jet SQL에서 지원 되지 않습니다.  
  
-   권한 부여 및 잠금 같은 보안 문  
  
-   집계 함수 참조를 사용 하 여 고유 값입니다.  
  
 다음 기능은 SQL-92로 지정 되지 않은 데스크톱 데이터베이스 드라이버에서 사용 된 SQL의 향상 된 기능을 보여 줍니다.  
  
-   크로스탭 쿼리에 대 한 지원을 제공 하는 변환 문입니다.  
  
-   추가 집계 함수 (**StDev** 하 고 **VarP**).  
  
> [!NOTE]  
>  데스크톱 데이터베이스 드라이버 지원할 표준 ANSI 구문을 백분율 (%) 및 _ (밑줄) * (별표) 및? (물음표)입니다.
