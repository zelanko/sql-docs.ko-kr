---
title: "매개 변수 데이터 형식 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], parameters
- parameter data type [ODBC]
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: fd7e99d8-d26a-408c-9733-6ffccde99f75
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5dcd41f599a6e57a55d05a8a869363ec70c5f756
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="parameter-data-types"></a>매개 변수 데이터 형식
각 매개 변수에 지정 된 경우에 **SQLBindParameter** 가 없습니다 내장 데이터 형식이 있을 경우 SQL 데이터 형식의 SQL 문의 매개 변수를 사용 하 여 정의 합니다. 따라서 다른 피연산자는 문에서 해당 데이터 형식을 유추할 수 있는 경우에 매개 변수 표식은 SQL 문에 포함할 수 있습니다. 와 같은 산술 식의 예를 들어? + 열 1을 나타내는 명명 된 열의 데이터 형식에서 COLUMN1, 매개 변수의 데이터 형식을 유추할 수 있습니다. 응용 프로그램 데이터 형식을 확인할 수 없는 경우 매개 변수 표식을 사용할 수 없습니다.  
  
 다음 표에서 한 몇 가지 유형의 매개 변수 s Q l-92에 맞게 데이터 형식을 결정 하는 방법에 대해 설명 합니다. 유추에 보다 포괄적인 사양에 대 한 매개 변수 형식과 다른 SQL 절에 사용 되는 경우에 SQL 92 사양을 참조 하십시오.  
  
|매개 변수의 위치|데이터 형식을 간주 됩니다.|  
|---------------------------|-----------------------|  
|이진 비교 또는 산술 연산자의 피연산자 하나|다른 피연산자와 동일|  
|첫 번째 피연산자는 **BETWEEN** 절|두 번째 피연산자와 동일|  
|두 번째 또는 세 번째 피연산자는 **BETWEEN** 절|첫 번째 피연산자와 동일|  
|함께 사용 하는 식을 **IN**|첫 번째 값 또는 하위 쿼리의 결과 열과 동일|  
|사용 하는 값 **IN**|식 또는 식에 매개 변수 표식이 있는 경우 첫 번째 값과 동일|  
|사용 하는 패턴 값 **같은**|VARCHAR|  
|함께 사용할 업데이트 값 **업데이트**|업데이트가 열과 동일|

