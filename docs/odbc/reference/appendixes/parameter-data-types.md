---
title: 매개 변수 데이터 형식 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], parameters
- parameter data type [ODBC]
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: fd7e99d8-d26a-408c-9733-6ffccde99f75
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.openlocfilehash: 5140c69184332b1760859421b7e802a5163a0f09
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100602"
---
# <a name="parameter-data-types"></a>매개 변수 데이터 형식
각 매개 변수에 지정 된 경우에 **SQLBindParameter** 은 입력 내장 데이터가 없을 경우 SQL 데이터 형식의 SQL 문에서 매개 변수를 사용 하 여 정의 합니다. 따라서 문에서 다른 피연산자에서 해당 데이터 형식을 유추할 수 있습니다. 경우에 매개 변수 표식은 SQL 문에 포함할 수 있습니다. 와 같은 산술 식의 예를 들어? + 열 1을 나타내는 명명 된 열의 데이터 형식에서 COLUMN1, 매개 변수의 데이터 형식을 유추할 수 있습니다. 응용 프로그램 데이터 형식을 확인할 수 없는 경우 매개 변수 표식을 사용할 수 없습니다.  
  
 다음 표에서 데이터 형식을 결정 하는 여러 유형의 SQL-92에 따라 매개 변수를 설명 합니다. 다른 SQL 절을 사용 하는 경우 매개 변수 형식 유추에 대 한 보다 포괄적인 사양, SQL-92 사양을 참조 하세요.  
  
|매개 변수의 위치|데이터 형식으로 간주|  
|---------------------------|-----------------------|  
|이항 연산 또는 비교 연산자의 피연산자 하나|다른 피연산자와 동일|  
|첫 번째 피연산자는 **BETWEEN** 절|두 번째 피연산자와 동일|  
|두 번째 또는 세 번째 피연산자는 **BETWEEN** 절|첫 번째 피연산자와 동일|  
|식을 사용한 **IN**|첫 번째 값 또는 하위 쿼리의 결과 열과 동일|  
|사용 되는 값 **IN**|식 또는 식에서 매개 변수 표식이 있으면 첫 번째 값과 동일|  
|사용 패턴을 **같은**|VARCHAR|  
|사용한 업데이트 값을 **업데이트**|업데이트 열과 동일|
