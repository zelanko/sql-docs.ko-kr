---
title: SELECT 문 제한 사항 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0cde0158e72d1e24c112c8e7955f0d6b317bd729
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67987854"
---
# <a name="select-statement-limitations"></a>SELECT 문 제한 사항
집계 함수 열은 SELECT 문에서 집합체가 아닌 열과 혼합할 수 없습니다.  
  
 GROUP BY 절이 있는 SELECT 문의 select 목록에는 GROUP BY 절 또는 set 함수의 식만 사용할 수 있습니다.  
  
 GROUP BY 절을 포함 하는 SELECT 문에서 별표를 사용 하 여 모든 열을 선택할 수 있는 것은 지원 되지 않습니다. 선택할 열의 이름을 지정 해야 합니다.  
  
 SELECT 문에서 세로 막대를 사용 하는 것은 지원 되지 않습니다. 세로 막대를 포함 하는 데이터 값을 참조 해야 하는 경우 SELECT 문에 매개 변수를 사용 합니다.  
  
 SELECT 문에서 열 별칭을 사용 하는 경우 "as" 라는 단어는 별칭 앞에와 야 합니다. 예를 들어, "a에서 a로 col1 선택"을 선택 합니다. "As"를 사용 하지 않을 경우 문은 오류를 반환 합니다.  
  
 SELECT 문에 잘못 된 열 이름을 입력 하면 sqlstate S0022 오류 "열을 찾을 수 없습니다." 대신 SQLSTATE 07001 오류가 반환 됩니다.  
  
 Microsoft Excel 드라이버를 사용 하는 경우 빈 문자열을 열에 삽입 하면 빈 문자열이 NULL로 변환 됩니다. WHERE 절에서 빈 문자열을 사용 하 여 실행 되는 검색 된 SELECT 문은 해당 열에서 실패 합니다.
