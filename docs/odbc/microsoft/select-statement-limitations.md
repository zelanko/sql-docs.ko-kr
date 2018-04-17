---
title: SELECT 문의 제한 사항 | Microsoft Docs
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
- ODBC SQL grammar, SELECT statement limitations
- SELECT statement limitations [ODBC]
ms.assetid: c6b05955-f8fd-4706-a1a7-a8dbd74870c2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5b36eae112c385cf5cc336640460c704b0bd205e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="select-statement-limitations"></a>SELECT 문의 제한 사항
SELECT 문에서 비 집계 열과 집계 함수 열을 혼합할 수 없습니다.  
  
 GROUP BY 절이 있는 SELECT 문의 select 목록에 GROUP BY 절에서 식을 하나만 사용할 수 있습니다 또는 함수를 설정 합니다.  
  
 GROUP BY 절이 포함 된 SELECT 문에서 별표 (모든 열을 선택)를 사용 하는 지원 되지 않습니다. 선택 열의 이름은 지정 해야 합니다.  
  
 SELECT 문에서 세로 막대를 사용 하는 지원 되지 않습니다. 세로 막대를 포함 하는 데이터 값을 참조 하는 경우 SELECT 문에 매개 변수를 사용 합니다.  
  
 SELECT 문에서 열 별칭을 사용할 경우 단어 "as" 별칭 앞에 야 합니다. 예를 들어 "으로 SELECT col1는 b에서." "와" 하지 않고 문이 오류가 반환 됩니다.  
  
 잘못 된 열 이름이 SELECT 문으로 입력 된 경우 "잘못 된 수의 매개 변수를" 오류를 SQLSTATE 07001 SQLSTATE S0022 오류 대신 "열 찾을 수 없습니다." 반환 됩니다.  
  
 빈 문자열이 null 인 경우 변환 됩니다 Microsoft Excel 드라이버를 사용 하면 빈 문자열은 열에 삽입 하는 경우, 검색 된 SELECT 문의 WHERE 절에는 빈 문자열에서 실행 되는 해당 열에 실패 합니다.
