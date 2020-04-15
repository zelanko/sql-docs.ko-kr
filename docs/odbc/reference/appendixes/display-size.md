---
title: 디스플레이 크기 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- display size of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- SQL data types [ODBC], column characteristics
ms.assetid: 9f7f766f-2492-463c-aab7-f2476e222042
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 578bf0cbdf2dd1dbd06dd4a248f4efa5eb839916
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307034"
---
# <a name="display-size"></a>표시 크기
열의 표시 크기는 문자 형식으로 데이터를 표시하는 데 필요한 최대 문자 수입니다. 다음 표는 각 ODBC SQL 데이터 형식에 대한 표시 크기를 정의합니다.  
  
|SQL 유형 식별자|디스플레이 크기|  
|-------------------------|------------------|  
|모든 문자 유형[a]|정의된(고정 된 형식의 경우) 또는 문자 형식으로 데이터를 표시하는 데 필요한 문자 수(가변 형식의 경우)입니다.|  
|SQL_DECIMAL SQL_NUMERIC|열과 2(기호, *정밀도* 숫자 및 소수점)의 정밀도입니다. 예를 들어 NUMERIC(10,3)으로 정의된 열의 표시 크기는 12입니다.|  
|SQL_BIT|1(1자리).|  
|SQL_TINYINT|4 서명된 경우(기호 및 3자리) 또는 서명되지 않은 경우(3자리)|  
|SQL_SMALLINT|6 서명된 경우(기호 및 5자리) 또는 5개의 서명되지 않은 경우(5자리).|  
|SQL_INTEGER|11 서명된 경우(서명 및 10자리) 또는 서명되지 않은 경우(10자리) 10.|  
|SQL_BIGINT|20(서명된 경우 기호 및 19자리 또는 서명되지 않은 경우 20자리).|  
|SQL_REAL|14(기호, 7자리, 소수점, 문자 *E,* 기호 및 2자리).|  
|SQL_FLOAT SQL_DOUBLE|24(기호, 15자리, 소수점, 문자 *E,* 기호 및 3자리).|  
|모든 바이너리 유형[a]|열 의 정의된 또는 최대(가변 형식의 경우) 길이는 2번입니다. (각 이진 바이트는 2자리 헥사데피만 숫자로 표시됩니다.)|  
|SQL_TYPE_DATE|10 *(형식yy-mm-dd형식의*날짜).|  
|SQL_TYPE_TIME|8 *(형식hh:mm:ss)*<br /><br /> -또는-<br /><br /> 9 + *s* *(hh:mm:ss*[.fff...]의 시간, *여기서 s는* 분수 초 정밀도입니다.).|  
|SQL_TYPE_TIMESTAMP|*19(yyy-mm-dd hh:mm:ss* 형식의 타임스탬프용)<br /><br /> -또는-<br /><br /> 20 + *s* *(yyyy-mm-dd hh:mm:mm:ss*[.fff...] 형식의 타임스탬프의 경우, *s는* 분수 초 정밀도입니다.)|  
|모든 간격 데이터 형식|[간격 데이터 형식 길이를](../../../odbc/reference/appendixes/interval-data-type-length.md)참조하십시오.|  
|SQL_GUID|*36(aaaaaaa-bbbb-cccc-dddd-eeeeeeeeeee eeeeeeee eeeeeee 형식의* 문자 수|  
  
 [a] 드라이버가 변수 형식의 열 또는 매개 변수 길이를 확인할 수 없는 경우 SQL_NO_TOTAL 반환합니다.
