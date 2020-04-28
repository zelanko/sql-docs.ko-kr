---
title: SQLPrepare (Visual FoxPro ODBC 드라이버) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301559"
---
# <a name="sqlprepare-visual-foxpro-odbc-driver"></a>SQLPrepare(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함 되어 있습니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 지원: 전체  
  
 ODBC API 규칙: 코어 수준  
  
 문을 최적화 하 고 실행 하는 방법을 계획 하 여 SQL 문을 준비 합니다. SQL 문은 [Sqlexecdirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)에 의해 실행 되도록 컴파일됩니다.  
  
 테이블, 뷰 또는 필드 이름에 공백이 포함 된 경우 큰따옴표 (')로 이름을 묶습니다. 예를 들어 데이터베이스에 내 테이블 이라는 테이블과 My Field 필드가 있는 경우 식별자의 각 요소를 다음과 같이 묶습니다.  
  
```  
SELECT * FROM `My Table`.`My Field`  
```  
  
 자세한 내용은 *ODBC 프로그래머 참조*에서 [sqlprepare](../../odbc/reference/syntax/sqlprepare-function.md) 를 참조 하세요.
