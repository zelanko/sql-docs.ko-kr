---
title: SQLPrepare (비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPrepare function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 0c4cb5a4-9729-4b2e-a0c6-52027b92e8fc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 14c9358d04e539eb2c77a00e195e8216cd0f5496
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301559"
---
# <a name="sqlprepare-visual-foxpro-odbc-driver"></a>SQLPrepare(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함되어 있습니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 지원: 전체  
  
 ODBC API 적합성: 코어 레벨  
  
 문을 최적화하고 실행하는 방법을 계획하여 SQL 문을 준비합니다. SQL 문은 [SQLExecDirect에](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)의해 실행을 위해 컴파일됩니다.  
  
 테이블, 뷰 또는 필드 이름에 공백이 포함된 경우 이름을 따옴표(') 마크로 둘러싸십시오. 예를 들어 데이터베이스에 내 테이블과 내 필드라는 테이블이 포함된 경우 식별자의 각 요소를 다음과 같이 둘러싸십시오.  
  
```  
SELECT * FROM `My Table`.`My Field`  
```  
  
 자세한 내용은 *ODBC 프로그래머의 참조에서* [SQLPrepare를](../../odbc/reference/syntax/sqlprepare-function.md) 참조하십시오.
