---
title: "선행 및 초의 전체 자릿수가 Interval 데이터 형식에 대 한 재정의 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: 3d65493f-dce7-4d29-9f59-c63a4e47918c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1ce549be1e3222f41615e5935418cf3e02e767a4
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>기본 선행 및 초의 전체 자릿수가 Interval 데이터 형식에 대 한 재정의
호출 하 여는 카드가의 SQL_DESC_TYPE 필드는 datetime 또는 간격 C 형식으로 설정 된 경우 **SQLBindCol** 또는 **SQLSetDescField**의 SQL_DESC_PRECISION 필드 (간격 (초)을 포함 합니다. 전체 자릿수)는 다음과 같은 기본값으로 설정 됩니다.  
  
-   타임 스탬프와 두 번째 구성 요소와 모든 interval 데이터 형식에 대 한 6입니다.  
  
-   다른 모든 데이터 형식에 대 한 0입니다.  
  
 모든 interval 데이터 형식에 대 한 간격 선행 필드 정밀도 담긴 SQL_DESC_DATETIME_INTERVAL_PRECISION 설명자 필드는 2의 기본 값으로 설정 됩니다.  
  
 호출 하 여 프로그램 APD의 SQL_DESC_TYPE 필드는 datetime 또는 간격 C 형식으로 설정 된 경우 **SQLBindParameter** 또는 **SQLSetDescField**, SQL_DESC_PRECISION 및 SQL_DESC_DATETIME_INTERVAL_ APD의 전체 자릿수 필드는 이전에 제공 된 기본값으로 설정 됩니다. 이러한 현상은 입력된 매개 변수에 대해 있지만 입/출력 또는 출력 매개 변수에 대 한 합니다.  
  
 에 대 한 호출 **SQLSetDescRec** 기본 전체 자릿수를 유도 하는 간격을 설정 하지만 간격 초의 전체 자릿수가 SQL_DESC_PRECISION 필드) (에서 값에 설정 하는 해당 *정밀도* 인수입니다.  
  
 지정 된 기본값 중 하나가 이전에 허용 되지 않는 경우 응용 프로그램, 응용 프로그램 호출 하 여 SQL_DESC_PRECISION 또는 SQL_DESC_DATETIME_INTERVAL_PRECISION 필드를 설정 해야 **SQLSetDescField**합니다.  
  
 응용 프로그램을 호출 하는 경우 **SQLGetData** 날짜/시간 또는 간격 C 형식으로 데이터를 반환 하는 기본 간격 선행 자릿수 및 간격 초의 전체 자릿수가 사용 됩니다. 기본값을 적용할 수 있는 응용 프로그램 호출 해야 합니다 **SQLSetDescField** 설명자 필드 중 하나를 설정 하려면 또는 **SQLSetDescRec** SQL_DESC_PRECISION 설정 하려면. 에 대 한 호출 **SQLGetData** 있어야는 *TargetType* 의 SQL_ARD_TYPE 설명자 필드에 값을 사용 하도록 합니다.  
  
 때 **SQLPutData** 호출 되는 호출에 대 한 APD 필드는 전체 자릿수 및 간격 초 전체 자릿수는 실행 시 데이터 매개 변수 또는 열에 해당 하는 설명자 레코드의 필드에서 읽은 유도 하는 간격 **SQLExecute** 또는 **SQLExecDirect**, 또는 필드에 대 한 호출 **SQLBulkOperations** 또는 **SQLSetPos**합니다.

