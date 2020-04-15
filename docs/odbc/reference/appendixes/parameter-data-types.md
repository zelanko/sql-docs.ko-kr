---
title: 매개 변수 데이터 유형 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.reviewer: ''
ms.openlocfilehash: f29bb70937df32e03480c13c7ef739eb273f15eb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303584"
---
# <a name="parameter-data-types"></a>매개 변수 데이터 형식
**SQLBindParameter로** 지정된 각 매개 변수는 SQL 데이터 형식을 사용하여 정의되지만 SQL 문의 매개 변수에는 본질적인 데이터 형식이 없습니다. 따라서 매개 변수 마커는 해당 데이터 형식을 명령문의 다른 피연산자에서 유추할 수 있는 경우에만 SQL 문에 포함할 수 있습니다. 예를 들어, 와 같은 산술 식에서 ? + COLUMN1, 매개 변수의 데이터 형식은 COLUMN1로 표현된 명명된 열의 데이터 형식으로부터 유추될 수 있다. 데이터 형식을 확인할 수 없는 경우 응용 프로그램은 매개 변수 마커를 사용할 수 없습니다.  
  
 다음 표에서는 SQL-92에 따라 여러 매개 변수 유형에 대해 데이터 형식이 결정되는 방법을 설명합니다. 다른 SQL 절을 사용할 때 매개 변수 형식을 유추하는 방법에 대한 보다 포괄적인 사양은 SQL-92 사양을 참조하십시오.  
  
|매개변수 위치|가정된 데이터 형식|  
|---------------------------|-----------------------|  
|이진 산술 연산또는 비교 연산자의 한 개의 카연드|다른 나연산자와 동일|  
|**BETWEEN** 절의 첫 번째 나연|두 번째 나연과 동일|  
|**BETWEEN** 절의 두 번째 또는 세 번째 진연|첫 번째 시연과 동일|  
|**IN과** 함께 사용되는 식|하위 쿼리의 첫 번째 값 또는 결과 열과 동일합니다.|  
|**IN과** 함께 사용되는 값|식에 매개 변수 마커가 있는 경우 식 또는 첫 번째 값과 동일합니다.|  
|**LIKE와** 함께 사용되는 패턴 값|VARCHAR|  
|**UPDATE와** 함께 사용되는 업데이트 값|업데이트 열과 동일|
