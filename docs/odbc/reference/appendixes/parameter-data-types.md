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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100602"
---
# <a name="parameter-data-types"></a>매개 변수 데이터 형식
**SQLBindParameter** 로 지정 된 각 매개 변수는 sql 데이터 형식을 사용 하 여 정의 되더라도 sql 문의 매개 변수에는 내장 데이터 형식이 없습니다. 따라서 매개 변수 표식은 문의 다른 피연산자에서 해당 데이터 형식을 유추할 수 있는 경우에만 SQL 문에 포함할 수 있습니다. 예를 들어?와 같은 산술 식에서 + COLUMN1, 매개 변수의 데이터 형식은 COLUMN1으로 표시 되는 명명 된 열의 데이터 형식에서 유추할 수 있습니다. 응용 프로그램은 데이터 형식을 확인할 수 없는 경우 매개 변수 표식을 사용할 수 없습니다.  
  
 다음 표에서는 SQL-92에 따라 여러 유형의 매개 변수에 대해 데이터 형식이 결정 되는 방법에 대해 설명 합니다. 다른 SQL 절을 사용할 때 매개 변수 유형을 유추 하는 방법에 대 한 보다 포괄적인 사양은 SQL-92 사양을 참조 하십시오.  
  
|매개 변수의 위치|가정 데이터 형식|  
|---------------------------|-----------------------|  
|이항 산술 연산자 또는 비교 연산자의 한 피연산자|다른 피연산자와 동일 합니다.|  
|**BETWEEN** 절의 첫 번째 피연산자|두 번째 피연산자와 동일 합니다.|  
|**BETWEEN** 절의 두 번째 또는 세 번째 피연산자|첫 번째 피연산자와 동일 합니다.|  
|**의에서** 사용 되는 식입니다.|하위 쿼리의 첫 번째 값 또는 결과 열과 동일 합니다.|  
|**에서** 사용 되는 값|식에 매개 변수 표식이 있는 경우 식과 동일 하거나 첫 번째 값입니다.|  
|**LIKE** 와 함께 사용 되는 패턴 값입니다.|VARCHAR|  
|**업데이트** 에 사용 되는 업데이트 값|업데이트 열과 동일|
