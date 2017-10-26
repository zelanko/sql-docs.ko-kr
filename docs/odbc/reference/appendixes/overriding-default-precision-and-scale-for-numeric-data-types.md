---
title: "기본 전체 자릿수 및 소수 자릿수 숫자 데이터 형식에 대 한 재정의 | Microsoft Docs"
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
- numeric data type [ODBC], precision and scale
- precision [ODBC], numeric data types
- data types [ODBC], numeric data types
- numeric data type [ODBC]
- numeric literals [ODBC]
ms.assetid: 84292334-0e33-4a1b-84de-8c018dd787f3
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 613ec65d838a525251b6682cca477c5c8d24a162
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>기본 전체 자릿수 및 소수 자릿수 숫자 데이터 형식에 대 한 재정의
호출 하 여 프로그램 카드가의 SQL_DESC_TYPE 필드 SQL_C_NUMERIC로 설정 되 면 **SQLBindCol** 또는 **SQLSetDescField**는 카드가에서 SQL_DESC_SCALE 필드를 0으로 설정 되 고 SQL_DESC_PRECISION 필드를 설정 에 기본 드라이버에서 정의 된 전체 자릿수입니다. 에 마찬가지입니다는 APD의 SQL_DESC_TYPE 필드를 호출 하 여 SQL_C_NUMERIC로 설정 하는 경우 **SQLBindParameter** 또는 **SQLSetDescField**합니다. 입력, 입/출력 또는 출력 매개 변수 마찬가지입니다.  
  
 설명 된 기본값 중 하나가 이전에 허용 되지 않는 응용 프로그램에 대 한 경우 응용 프로그램 호출 하 여 SQL_DESC_PRECISION 또는 SQL_DESC_SCALE 필드를 설정 해야 **SQLSetDescField** 또는 **SQLSetDescRec**.  
  
 응용 프로그램을 호출 하는 경우 **SQLGetData** SQL_C_NUMERIC 구조로 데이터를 반환 하려면 기본 자릿수가 SQL_DESC_SCALE 및 SQL_DESC_PRECISION 필드를 사용 합니다. 기본값이 허용 되지 않는 경우에 응용 프로그램 호출 해야 **SQLSetDescRec** 또는 **SQLSetDescField** 필드를 설정 하 여 호출 **SQLGetData** 는 와*TargetType* 의 SQL_ARD_TYPE 설명자 필드에 값을 사용 하도록 합니다.  
  
 때 **SQLPutData** 은 실행 시 데이터 매개 변수 또는 열에 해당 하는 설명자 레코드의 자릿수가 SQL_DESC_SCALE 및 SQL_DESC_PRECISION 필드를 사용 하 여 호출을 호출 하는 APD 필드에 대 한 호출 ** SQLExecute** 또는 **SQLExecDirect**, 또는 필드에 대 한 호출 **SQLBulkOperations** 또는 **SQLSetPos**합니다.

