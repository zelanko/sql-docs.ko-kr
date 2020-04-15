---
title: 간격 데이터 유형에 대한 선행 및 초 정밀도 재정재의 재정의 | 마이크로 소프트 문서
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
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: 3d65493f-dce7-4d29-9f59-c63a4e47918c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1e60d5d8fc696ad8e2bd4cfb0c082ff214e066d0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303604"
---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>간격 데이터 형식에 대한 기본 선행 및 초 전체 자릿수 재정의
ARD의 SQL_DESC_TYPE 필드가 날짜 시간 또는 간격 C 유형으로 설정되면 **SQLBindCol** 또는 **SQLSetDescField를**호출하여 SQL_DESC_PRECISION 필드(간격 초 정밀도 포함)는 다음과 같은 기본값으로 설정됩니다.  
  
-   타임스탬프 및 두 번째 구성 요소가 있는 모든 간격 데이터 형식의 경우 6입니다.  
  
-   다른 모든 데이터 형식에 대해 0입니다.  
  
 모든 간격 데이터 형식에 대해 SQL_DESC_DATETIME_INTERVAL_PRECISION 설명자 필드는 구간 선행 필드 정밀도를 포함하며 기본값 2로 설정됩니다.  
  
 APD의 SQL_DESC_TYPE 필드가 날짜 시간 또는 간격 C 유형으로 설정되면 **SQLBindParameter** 또는 **SQLSetDescField를**호출하여 APD의 SQL_DESC_PRECISION 및 SQL_DESC_DATETIME_INTERVAL_PRECISION 필드는 이전에 제공된 기본값으로 설정됩니다. 입력 매개 변수는 마찬가지이지만 입력/출력 또는 출력 매개변수는 그렇지 않습니다.  
  
 **SQLSetDescRec에** 대한 호출은 정밀도를 기본값으로 이어지는 간격을 설정하지만 간격 초 정밀도(SQL_DESC_PRECISION 필드의)를 *Precision* 인수 값으로 설정합니다.  
  
 이전에 제공된 기본값 중 하나가 응용 프로그램에 허용되지 않는 경우 응용 프로그램은 **SQLSetDescField**를 호출하여 SQL_DESC_PRECISION 또는 SQL_DESC_DATETIME_INTERVAL_PRECISION 필드를 설정해야 합니다.  
  
 응용 프로그램에서 **SQLGetData를** 호출하여 데이터를 날짜 시간 또는 간격 C 유형으로 반환하는 경우 정밀도와 간격 초 정밀도를 선도하는 기본 간격이 사용됩니다. 두 기본값 중 하나를 사용할 수 없는 경우 응용 프로그램은 **SQLSetDescField를** 호출하여 설명자 필드를 설정하거나 **SQLSetDescRec를** 호출하여 SQL_DESC_PRECISION 설정해야 합니다. **SQLGetData에** 대 한 호출에는 설명자 필드의 값을 사용 하는 *SQL_ARD_TYPE TargetType이* 있어야 합니다.  
  
 **SQLPutData가** 호출될 때, 간격 선행 정밀도와 간격 초 정밀도는 **SQLExecute** 또는 **SQLExecDirect에**대한 호출에 대한 APD 필드인 실행 시 데이터 매개 변수 또는 열에 해당하는 설명자 레코드의 필드에서 읽히거나 **SQLBulkOperations** 또는 **SQLSetPos**에 대한 호출을 위한 ARD 필드입니다.
