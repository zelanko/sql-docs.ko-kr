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
manager: craigg
ms.openlocfilehash: 26bf17596dbd3279498df2edcee7636db95ae139
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47767221"
---
# <a name="select-statement-limitations"></a>SELECT 문 제한 사항
SELECT 문에서 비 집계 열이 있는 열을 집계 함수를 혼합할 수 없습니다.  
  
 GROUP BY 절이 있는 SELECT 문의 select 목록에 GROUP BY 절에서 식을 하나만 사용할 수 있습니다 하거나 함수를 설정 합니다.  
  
 GROUP BY 절이 포함 된 SELECT 문에서 별표 (모든 열을 선택)를 사용 하 여 지원 되지 않습니다. 선택 열의 이름은 지정 해야 합니다.  
  
 SELECT 문에서 세로 막대의 사용이 지원 되지 않습니다. 세로 막대를 포함 하는 데이터 값을 참조 하는 경우에 SELECT 문에서 매개 변수를 사용 합니다.  
  
 SELECT 문에서 열 별칭을 사용 하는 경우 단어 "as" 별칭 앞에 야 합니다. 예를 들어 "SELECT col1으로는 b에서." 합니다 "와" 하지 않고 문이 오류를 반환 합니다.  
  
 "잘못 된 수의 매개 변수를" 오류를 SQLSTATE 07001 SQLSTATE S0022 오류 대신 "열 Not Found."이 반환 됩니다 SELECT 문으로 잘못 된 열 이름을 입력 하는 경우  
  
 빈 문자열을 NULL 변환할 Microsoft Excel 드라이버를 사용 하면 빈 문자열 열에 삽입 하는 경우, 해당 열에 WHERE 절에 빈 문자열을 사용 하 여 실행 되는 SELECT 문의 검색된에 실패 합니다.
