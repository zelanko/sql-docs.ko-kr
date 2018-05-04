---
title: 간격 데이터 형식의 전체 자릿수 | Microsoft Docs
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
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 73acf5a46768b11b0eb223327c1fa1bcf0e49f68
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="interval-data-type-precision"></a>간격 데이터 유형 정밀도
간격 데이터 형식의 전체 자릿수는 전체 자릿수, 간격 정밀도 및 초의 전체 자릿수를 유도 하는 간격을 포함 합니다.  
  
 간격의 선행 필드 부호 있는 숫자입니다. 선행 필드에 대 한 최대 자릿수 호출 양에 따라 결정 됩니다 *전체 자릿수를 유도 하는 간격* 데이터 형식 선언에 포함 되어 있는 합니다. 예를 들어 선언: 간격 HOUR(5) 분으로 5;의 전체 자릿수를 유도 하는 간격에 시간 필드 99999 통해 –99999에서는 값을 사용할 수 있습니다. 전체 자릿수를 유도 하는 간격 설명자 레코드의 SQL_DESC_DATETIME_INTERVAL_PRECISION 필드에 포함 되어 있습니다.  
  
 필드의 간격 데이터 형식으로 구성 된 목록 이라고 *간격 정밀도*합니다. 알 수 있듯이 "precision" 라는 용어 수는 숫자 값을 않습니다. 간격 일 TO 형식의 간격 정밀도 목록 일, 시, 두 번째가 되는 예를 들어, 분, 초입니다. 이 값을 보유 하는 설명자 필드가 없으면 간격 정밀도 간격 데이터 형식이 항상 확인할 수 있습니다.  
  
 두 번째 필드에 있는 모든 간격 데이터 형식에는 *초의 정밀도*합니다. 소수 자릿수 초 값의 소수 부분에 허용 되는 수입니다. 이것이 다른 데이터 형식에 대 한 다른 여기서 정밀도 소수점 전의 자릿수를 나타냅니다. 간격 데이터 형식의 초 전체 자릿수는 소수점 뒤 자릿수는 합니다. 예를 들어 초 전체 자릿수는 6으로 설정, 있으면.123456 및 번호 1230.001230으로 해석 되으로 번호에서 분수 필드에서 123456 해석 합니다. 다른 데이터 형식에 대 한이 라고 눈금. 간격 초의 전체 자릿수가 SQL_DESC_PRECISION 설명자 필드에 포함 되어 있습니다. SQL 간격 값의 소수 자릿수 초 구성 요소 전체 자릿수 C 간격 구조에 보유할 수 무엇 보다 크면 드라이버-정의 된 SQL 간격에 소수 자릿수 초 값은 C로 변환 될 때 잘립니다 반올림 여부 간격 구조입니다.  
  
 SQL_DESC_TYPE 필드 SQL_INTERVAL 설정은 SQL_DESC_CONCISE_TYPE 필드 간격 데이터 형식으로 설정 되 면는 값을 SQL_DESC_DATETIME_INTERVAL_CODE 간격 데이터 형식에 대 한 코드로 설정 됩니다. SQL_DESC_DATETIME_INTERVAL_PRECISION 필드는 2의 기본 간격 선행 정밀도로 자동으로 설정 하 고 SQL_DESC_PRECISION 필드 간격 (초)의 기본 정밀도 6으로 자동 설정 됩니다. 응용 프로그램에 대 한 호출을 통해 설명자 필드를 명시적으로 설정 해야 이러한 값 중 하나 없는 경우 적절 한 **SQLSetDescField**합니다.
