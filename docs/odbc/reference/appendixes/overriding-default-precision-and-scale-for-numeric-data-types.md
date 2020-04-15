---
title: 숫자 데이터 유형에 대한 기본 정밀도 및 배율 재정의 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], precision and scale
- precision [ODBC], numeric data types
- data types [ODBC], numeric data types
- numeric data type [ODBC]
- numeric literals [ODBC]
ms.assetid: 84292334-0e33-4a1b-84de-8c018dd787f3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 365c5f69d21dd3a4ad8e89805d81f1b3b0c9dcba
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303594"
---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>숫자 데이터 형식에 대한 기본 전체 자릿수 및 소수 자릿수 재정의
ARD의 SQL_DESC_TYPE 필드가 **SQLBindCol** 또는 **SQLSetDescField를**호출하여 SQL_C_NUMERIC 설정되면 ARD의 SQL_DESC_SCALE 필드가 0으로 설정되고 SQL_DESC_PRECISION 필드가 드라이버 정의 기본 정밀도로 설정됩니다. APD의 SQL_DESC_TYPE 필드가 **SQLBindParameter** 또는 **SQLSetDescField**를 호출하여 SQL_C_NUMERIC 설정된 경우에도 마찬가지입니다. 이는 입력, 입력/출력 또는 출력 매개변수에 해당합니다.  
  
 앞에서 설명한 기본값 중 하나가 응용 프로그램에 허용되지 않는 경우 응용 프로그램은 **SQLSetDescField** 또는 **SQLSetDescRec**을 호출하여 SQL_DESC_SCALE 또는 SQL_DESC_PRECISION 필드를 설정해야 합니다.  
  
 응용 프로그램에서 **SQLGetData를** 호출하여 데이터를 SQL_C_NUMERIC 구조로 반환하면 기본 SQL_DESC_SCALE 및 SQL_DESC_PRECISION 필드가 사용됩니다. 기본값을 사용할 수 없는 경우 응용 프로그램은 **SQLSetDescRec** 또는 **SQLSetDescField를** 호출하여 필드를 설정한 다음 **sqlGetData를** *SQL_ARD_TYPE TargetType을* 호출하여 설명자 필드의 값을 사용해야 합니다.  
  
 **SQLPutData가** 호출될 때 호출은 **SQLExecute** 또는 **SQLExecDirect**에 대한 호출에 대한 APD 필드인 실행 시 데이터 매개 변수 또는 열에 해당하는 설명자 레코드의 SQL_DESC_SCALE 및 SQL_DESC_PRECISION 필드를 사용하거나 **SQLBulkOperations** 또는 **SQLSetPos에**대한 호출에 대한 ARD 필드를 사용합니다.
