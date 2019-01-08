---
title: 간격 데이터 형식 전체 자릿수 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: a8df4339ae30b9058e5a5864c37807c6b02e4fdd
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52532117"
---
# <a name="interval-data-type-precision"></a>간격 데이터 형식 전체 자릿수
전체 자릿수는 간격 데이터 형식에 대 한 전체 자릿수, 전체 자릿수 간격 및 초 전체 자릿수를 유도 하는 간격을 포함 합니다.  
  
 선행 간격 필드는 부호 있는 숫자입니다. 선행 필드에 대 한 최대 자릿수는 호출을 수량에 따라 결정 됩니다 *전체 자릿수를 유도 하는 간격* 데이터 형식 선언의 일부인 합니다. 예를 들어 선언: 간격 HOUR(5) 분으로가 간격 선행 자릿수 5; 시간 필드에서 99999-99999 값을 사용할 수 있습니다. 전체 자릿수를 유도 하는 간격 설명자 레코드의 SQL_DESC_DATETIME_INTERVAL_PRECISION 필드에 포함 됩니다.  
  
 간격 데이터 형식으로 구성 된 필드의 목록 이라고 *간격 정밀도*합니다. "Precision" 라는 용어 수 있듯이 숫자 값, 아닙니다. 예를 들어, INTERVAL DAY TO 형식의 간격 정밀도 둘째 목록인 일, 시간, 분, 초입니다. 이 값을 보유 하는 설명자 필드가 없습니다. 간격 정밀도 간격 데이터 형식에 의해 항상 확인할 수 있습니다.  
  
 두 번째 필드에 있는 모든 간격 데이터 형식에는 *초의 정밀도*합니다. 소수 자릿수 초 값의 소수 부분에 사용할 수입니다. 이것이 다른 데이터 형식에 대 한 다른 여기서 전체 자릿수는 소수점 전의 자릿수를 나타냅니다. 초 전체 자릿수 간격 데이터 형식의 경우 소수 자릿수는 소수점 뒤 예를 들어, 초 전체 자릿수를 6으로 설정 된 경우 번호에서 분수 필드는 123456 해석 됩니다 대로.123456 및 1230.001230으로 해석 됩니다. 다른 데이터 형식에 대 한이 이라고를 확장 합니다. 간격 초의 전체 자릿수가 SQL_DESC_PRECISION 설명자 필드에 포함 됩니다. SQL 간격 값의 소수 자릿수 초 구성 요소 전체 자릿수 보다 크면 C 간격 구조에 보관할 수 있습니다, 드라이버-정의 된 SQL 간격의 초 소수 부분 값은 C로 변환 될 때 잘립니다 반올림 여부 간격 구조입니다.  
  
 SQL_DESC_TYPE 필드 SQL_INTERVAL로 SQL_DESC_CONCISE_TYPE 필드 간격 데이터 형식으로 설정 되 면을 SQL_DESC_DATETIME_INTERVAL_CODE 간격 데이터 형식에 대 한 코드에 설정 됩니다. SQL_DESC_DATETIME_INTERVAL_PRECISION 필드 2의 기본 간격 선행 정밀도로 자동 설정 됩니다 및 SQL_DESC_PRECISION 필드 6 기본 간격 초 전체 자릿수를 자동으로 설정 됩니다. 응용 프로그램에 대 한 호출을 통해 설명자 필드를 명시적으로 설정 해야 적절 한 다음이 값 중 하나가 없으면 **SQLSetDescField**합니다.
