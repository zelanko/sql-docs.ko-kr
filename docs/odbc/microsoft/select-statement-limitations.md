---
title: 문 제한 사항 선택 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, SELECT statement limitations
- SELECT statement limitations [ODBC]
ms.assetid: c6b05955-f8fd-4706-a1a7-a8dbd74870c2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d91e93076a67287cbbd2b64b2ad0d6414a0aea6d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300923"
---
# <a name="select-statement-limitations"></a>SELECT 문 제한 사항
집계 함수 열은 SELECT 문의 비집계 열과 혼합할 수 없습니다.  
  
 GROUP BY 절이 있는 SELECT 문의 선택 목록에는 GROUP BY 절 또는 설정 함수의 표현식만 있을 수 있습니다.  
  
 GROUP BY 절을 포함하는 SELECT 문에서 별표(모든 열을 선택)의 사용은 지원되지 않습니다. 선택할 열의 이름을 지정해야 합니다.  
  
 SELECT 문에서 세로 막대의 사용은 지원되지 않습니다. 세로 막대가 포함된 데이터 값을 참조해야 하는 경우 SELECT 문에서 매개 변수를 사용합니다.  
  
 SELECT 문에서 열 별칭을 사용하는 경우 "as"라는 단어가 별칭 앞에 와야 합니다. 예를 들어 "col1을 b에서 로 선택합니다." "as"가 없으면 명령문이 오류를 반환합니다.  
  
 SELECT 문에 잘못된 열 이름을 입력하면 SQLSTATE S0022 오류인 "열을 찾을 수 없습니다"대신 SQLSTATE 07001 오류인 "잘못된 수의 매개 변수"가 반환됩니다.  
  
 Microsoft Excel 드라이버를 사용하면 빈 문자열이 열에 삽입되면 빈 문자열이 NULL로 변환됩니다. WHERE 절의 빈 문자열로 실행되는 검색된 SELECT 문은 해당 열에서 성공하지 못합니다.
