---
title: 간격 데이터 형식 정밀도 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- precision [ODBC]
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: eb73bd77-2e7e-4498-a266-4d7c990a0d56
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 746293c545c47917abd084ec3eb105051fc2fbcf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290743"
---
# <a name="interval-data-type-precision"></a>간격 데이터 형식 전체 자릿수
간격 데이터 형식의 정밀도에는 간격 선행 정밀도, 간격 정밀도 및 초 정밀도가 포함됩니다.  
  
 간격의 선행 필드는 서명된 숫자입니다. 선행 필드의 최대 자릿수는 데이터 형식 선언의 일부인 *간격 선행 정밀도라는* 수량에 의해 결정됩니다. 예를 들어, 선언: INTERVAL HOUR(5) to MINUTE는 간격 을 선도하는 정밀도5를 가합니다. HOUR 필드는 -99999 ~ 99999값을 사용할 수 있습니다. 선행 정밀도 간격은 설명자 레코드의 SQL_DESC_DATETIME_INTERVAL_PRECISION 필드에 포함됩니다.  
  
 간격 데이터 형식이 구성된 필드 목록을 간격 *정밀도라고*합니다. "정밀도"라는 용어가 암시할 수 있듯이 숫자 값이 아닙니다. 예를 들어, 인터벌 데이에서 second까지의 간격 정밀도는 일, 시간, 분, 초 목록입니다. 이 값을 보유하는 설명자 필드가 없습니다. 간격 정밀도는 항상 간격 데이터 형식에 의해 결정될 수 있습니다.  
  
 SECOND 필드가 있는 모든 간격 데이터 형식에는 *초 정밀도가*있습니다. 초 값의 소수 부분에 허용되는 소수 자릿수입니다. 이는 소수점 앞의 자릿수를 정밀도가 나타내는 다른 데이터 형식과 다릅니다. 간격 데이터 형식의 초 정밀도는 소수점 다음의 자릿수입니다. 예를 들어 초 정밀도가 6으로 설정된 경우 분수 필드의 숫자 123456은 .123456으로 해석되고 숫자 1230은 .001230으로 해석됩니다. 다른 데이터 형식의 경우 이를 축척이라고 합니다. 간격 초 정밀도는 설명자의 SQL_DESC_PRECISION 필드에 포함되어 있습니다. SQL 간격 값의 분수 초 구성 요소의 정밀도가 C 간격 구조에서 보유할 수 있는 값보다 큰 경우, C 간격 구조로 변환될 때 SQL 간격의 분수 초 값이 반올림되거나 잘린지 여부를 드라이버 정의합니다.  
  
 SQL_DESC_CONCISE_TYPE 필드가 간격 데이터 유형으로 설정되면 SQL_DESC_TYPE 필드가 SQL_INTERVAL 설정되고 SQL_DESC_DATETIME_INTERVAL_CODE 간격 데이터 형식의 코드로 설정됩니다. SQL_DESC_DATETIME_INTERVAL_PRECISION 필드는 정밀도를 2로 이끄는 기본 간격으로 자동으로 설정되고 SQL_DESC_PRECISION 필드는 기본 간격 초 정밀도 6으로 자동으로 설정됩니다. 이러한 값 중 하나가 적절하지 않은 경우 응용 프로그램은 **SQLSetDescField**에 대한 호출을 통해 설명자 필드를 명시적으로 설정해야 합니다.
