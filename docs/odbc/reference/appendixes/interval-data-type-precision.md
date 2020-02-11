---
title: Interval 데이터 형식 전체 자릿수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3424c58d25be69d2ddc42a3088aa457ebddf1d4b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67947608"
---
# <a name="interval-data-type-precision"></a>간격 데이터 형식 전체 자릿수
간격 데이터 형식에 대 한 전체 자릿수는 간격 선행 전체 자릿수, 간격 전체 자릿수, 초 정밀도를 포함 합니다.  
  
 간격의 선행 필드는 부호 있는 숫자입니다. 선행 필드의 최대 자릿수는 데이터 형식 선언의 일부인 *interval 선행 전체 자릿수* 라는 수량에 따라 결정 됩니다. 예를 들어, 시간 간격 시간 (5)을 분으로 설정한 경우 간격의 선행 전체 자릿수가 5가 됩니다. 시간 필드에는-99999에서 99999 까지의 값을 사용할 수 있습니다. 간격 선행 전체 자릿수는 설명자 레코드의 SQL_DESC_DATETIME_INTERVAL_PRECISION 필드에 포함 되어 있습니다.  
  
 간격 데이터 형식을 구성 하는 필드 목록을 *간격 전체 자릿수*라고 합니다. "전체 자릿수" 라는 용어는 숫자 값이 아닙니다. 예를 들어, INTERVAL DAY의 interval 전체 자릿수는 일, 시, 분, 초 목록입니다. 이 값을 보유 하는 설명자 필드가 없습니다. 간격 정밀도는 항상 interval 데이터 형식에 의해 결정 될 수 있습니다.  
  
 두 번째 필드가 있는 간격 데이터 형식의 *전체 자릿수는 초*입니다. 초 값의 소수 부분에 허용 되는 10 진수 숫자입니다. 이는 다른 데이터 형식에 대 한 것과 다릅니다. 여기서 precision은 소수점 앞의 자릿수를 나타냅니다. Interval 데이터 형식의 초 전체 자릿수는 소수점 뒤의 자릿수입니다. 예를 들어 초 전체 자릿수가 6으로 설정 된 경우 분수 필드의 숫자 123456는 123456로 해석 되 고 숫자 1230는. 001230로 해석 됩니다. 다른 데이터 형식의 경우이를 scale 이라고 합니다. 간격 (초)의 전체 자릿수는 설명자의 SQL_DESC_PRECISION 필드에 포함 됩니다. SQL interval 값의 소수 자릿수 초 구성 요소에 대 한 전체 자릿수가 C interval 구조에서 보유할 수 있는 것 보다 큰 경우, 해당 값은 C로 변환 될 때 SQL 간격의 소수 자릿수 초 값을 반올림 하거나 잘라낼 지 여부를 드라이버에서 정의 합니다. 간격 구조.  
  
 SQL_DESC_CONCISE_TYPE 필드가 interval 데이터 형식으로 설정 되어 있으면 SQL_DESC_TYPE 필드가 SQL_INTERVAL로 설정 되 고 SQL_DESC_DATETIME_INTERVAL_CODE이 interval 데이터 형식에 대 한 코드로 설정 됩니다. SQL_DESC_DATETIME_INTERVAL_PRECISION 필드는 자동으로 기본 간격 (2)으로 설정 되 고, SQL_DESC_PRECISION 필드는 자동으로 기본 간격 (초) 전체 자릿수 (6)로 설정 됩니다. 이러한 값 중 하나가 적절 하지 않은 경우 응용 프로그램은 **SQLSetDescField**를 호출 하 여 설명자 필드를 명시적으로 설정 해야 합니다.
