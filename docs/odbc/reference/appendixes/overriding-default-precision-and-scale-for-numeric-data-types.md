---
title: 기본 자릿수와 소수 자릿수 숫자 데이터 형식에 대 한 재정의 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f071cf4391c760f7d269382537c3cd4f2b758c3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63278306"
---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>숫자 데이터 형식에 대한 기본 전체 자릿수 및 소수 자릿수 재정의
호출 하 여 SQL_DESC_TYPE 필드는 카드가 SQL_C_NUMERIC로 설정 되 면 **SQLBindCol** 하거나 **SQLSetDescField**는 카드가 자릿수가 SQL_DESC_SCALE 필드는 0으로 설정 되어 및 SQL_DESC_PRECISION 필드가 설정 되 고, 에 기본 드라이버에서 정의 된 전체 자릿수입니다. 에 마찬가지는 APD의 SQL_DESC_TYPE 필드 중 하나를 호출 하 여 SQL_C_NUMERIC로 설정 된 경우 **SQLBindParameter** 하거나 **SQLSetDescField**합니다. 입력, 입/출력 또는 출력 매개 변수는 것과 마찬가지입니다.  
  
 설명 된 기본값 중 이전에 허용 되지 않는 응용 프로그램의 경우 응용 프로그램 호출 하 여 자릿수가 SQL_DESC_SCALE 또는 SQL_DESC_PRECISION 필드를 설정 해야 **SQLSetDescField** 또는 **SQLSetDescRec**.  
  
 응용 프로그램을 호출 하는 경우 **SQLGetData** SQL_C_NUMERIC 구조로 데이터를 반환 하는 기본 자릿수가 SQL_DESC_SCALE 및 자릿수가 SQL_DESC_PRECISION 필드를 사용 합니다. 기본값 허용 되지 않는 경우에 응용 프로그램 호출 해야 합니다 **SQLSetDescRec** 하거나 **SQLSetDescField** 필드를 설정 하 여 호출 **SQLGetData** 를사용하여*TargetType* 설명자 필드에 값을 사용 하도록 SQL_ARD_TYPE입니다.  
  
 때 **SQLPutData** 은 실행 시 데이터 매개 변수 또는 열에 해당 하는 설명자 레코드의 자릿수가 SQL_DESC_SCALE 및 자릿수가 SQL_DESC_PRECISION 필드를 사용 하 여 호출 호출에 대 한 호출에 대 한 APD 필드는  **SQLExecute** 또는 **SQLExecDirect**, 또는 필드에 대 한 호출 **SQLBulkOperations** 하거나 **SQLSetPos**합니다.
