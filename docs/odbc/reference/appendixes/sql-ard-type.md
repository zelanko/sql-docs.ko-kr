---
title: SQL_ARD_TYPE | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], SQL_ARD_TYPE
- SQL_ARD_TYPE [ODBC]
ms.assetid: 8d87ca10-f955-4284-8689-e9f4cc31e7ae
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7e021086561f0af45ddab1bd9ab777267ae515dd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlardtype"></a>SQL_ARD_TYPE
버퍼의 데이터는 카드가의 SQL_DESC_CONCISE_TYPE 필드에 지정 된 형식의 될 것임을 나타내려면 SQL_ARD_TYPE 유형 식별자를 사용 합니다. SQL_ARD_TYPE에 입력 된 *TargetType* 에 대 한 호출의 인수 **SQLGetData** 특정 데이터 형식 및 응용 프로그램 데이터를 변경 하는 버퍼의 설명자를 변경 하 여 입력을 사용 하도록 설정 하는 대신 필드입니다. 이 값의 데이터 형식에 연결 된  *\*TargetValuePtr* 버퍼 설명자 필드입니다. (SQL_ARD_TYPE에 대 한 호출에 입력 되지 않은 **SQLBindCol** 또는 **SQLBindParameter** 바운드 버퍼의 형식이 SQL_DESC_TYPE와 SQL_DESC_CONCISE_TYPE 필드에 이미 연결 되어 있고 변경할 수 있습니다 언제 든 지 이러한 필드 중 하나를 변경 하 여.)  
  
 선행 자릿수와 간격 데이터 형식의 전체 자릿수 (초)에 대 한 기본이 아닌 값을 지정 하는 SQL_ARD_TYPE 유형 식별자를 사용할 수 있습니다 및 SQL_C_NUMERIC 데이터에 대 한 전체 자릿수 및 소수 자릿수 값을 입력 합니다. 자세한 내용은 참조 [선행 기본 재정의 및 Interval 데이터 형식에 대 한 초의 전체 자릿수가](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md) 및 [재정의 기본 전체 자릿수 및 소수 자릿수 숫자 데이터 형식에 대해](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md)이 부록의 뒷부분에 나오는 합니다.
