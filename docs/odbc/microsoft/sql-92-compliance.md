---
title: SQL-92 준수 | Microsoft Docs
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
ms.openlocfilehash: e5d8ed2818b466d16591be8b70478221d7ac84df
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063376"
---
# <a name="sql-92-compliance"></a>SQL-92 호환성
ODBC 데스크톱 데이터베이스 드라이버와 기본 Microsoft Jet 엔진은 SQL-92 규격이 아닙니다. SQL-92에 정의 된 많은 기능을 지원 합니다. 드라이버에서 지원 되는 일부 기능은 SQL-92에서 지원 되지 않습니다. 자세한 내용은 *Microsoft Jet 데이터베이스 엔진 프로그래머 가이드*를 참조 하세요. 다음은 두 가지 주요 차이점입니다.  
  
-   데스크톱 데이터베이스 드라이버에서 사용 하는 SQL은 SQL-92에 지정 된 것 보다 더 강력한 식을 지원 합니다.  
  
-   BETWEEN 조건자에는 다른 규칙이 적용 됩니다.  
  
-   데스크톱 데이터베이스 드라이버와 ANSI SQL에서 사용 하는 SQL은 다른 키워드를 지원 합니다.  
  
 다음 SQL-92 기능은 Microsoft Jet SQL에서 지원 되지 않습니다.  
  
-   GRANT 및 LOCK과 같은 보안 문  
  
-   집계 함수 참조를 사용 하는 고유 합니다.  
  
 다음 기능은 SQL-92에 지정 되지 않은 데스크톱 데이터베이스 드라이버에서 사용 하는 SQL의 향상 된 기능입니다.  
  
-   크로스탭 쿼리에 대 한 지원을 제공 하는 TRANSFORM 문입니다.  
  
-   추가 집계 함수 (**StDev** 및 **VarP**)  
  
> [!NOTE]  
>  데스크톱 데이터베이스 드라이버는 * (별표) 및?가 아니라% (percent) 및 _ (밑줄)에 대 한 표준 ANSI 구문을 지원 합니다. (물음표)를 표시 합니다.
