---
title: SQLExecDirect (비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExecDirect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5004060f-8510-4018-87a4-d41789e69d3e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 40c0a3404a3e7a9a67b6f71d197343eddb417955
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298673"
---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함되어 있습니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 지원: 전체  
  
 ODBC API 적합성: 코어 레벨  
  
 예비 SQL 문을 새로 [실행합니다.](../../odbc/microsoft/visual-foxpro-terminology.md) Visual FoxPro ODBC 드라이버는 문안에 매개 변수가 있는 경우 매개 변수 마커 변수의 현재 값을 사용합니다.  
  
 한 번에 두 개 이상의 SQL 문을 제출하는 일괄 처리 명령을 만들려면 세미콜론(;)을 사용합니다. 을 사용하여 배치의 각 SQL 문을 분리합니다.  
  
 테이블, 뷰 또는 필드 이름에 공백이 포함된 경우 이름을 따옴표로 둘러싸십시오. 예를 들어 데이터베이스에 내 테이블과 내 필드라는 테이블이 포함된 경우 식별자의 각 요소를 다음과 같이 둘러싸십시오.  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 자세한 내용은 *ODBC 프로그래머의 참조에서* [SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md) 를 참조하십시오.
