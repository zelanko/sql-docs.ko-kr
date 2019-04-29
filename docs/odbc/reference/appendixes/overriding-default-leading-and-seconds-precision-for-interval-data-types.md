---
title: 간격 데이터 형식에 대 한 선행 및 초 전체 자릿수 재정의 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fdab9e6e60311aca4ce0ae35f92e38c45fdf3702
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63018478"
---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>간격 데이터 형식에 대한 기본 선행 및 초 전체 자릿수 재정의
호출 하 여는 카드가의 SQL_DESC_TYPE 필드는 datetime 또는 간격 C 형식으로 설정 하면 **SQLBindCol** 하거나 **SQLSetDescField**, SQL_DESC_PRECISION 필드 (포함 하는 간격 (초) 전체 자릿수)는 다음 기본값으로 설정 됩니다.  
  
-   두 번째 구성 요소를 사용 하 여 모든 간격 데이터 형식 및 타임 스탬프는 6입니다.  
  
-   다른 모든 데이터 형식에 대 한 0입니다.  
  
 모든 간격 데이터 형식에 대 한 간격 선행 필드 전체 자릿수를 포함 하는 SQL_DESC_DATETIME_INTERVAL_PRECISION 설명자 필드는 2의 기본 값으로 설정 됩니다.  
  
 호출 하 여는 APD의 SQL_DESC_TYPE 필드는 datetime 또는 간격 C 형식으로 설정 하면 **SQLBindParameter** 하거나 **SQLSetDescField**, SQL_DESC_PRECISION 및 SQL_DESC_DATETIME_INTERVAL_ APD의 전체 자릿수 필드는 이전에 지정 된 기본값으로 설정 됩니다. 마찬가지 입/출력 또는 출력 매개 변수가 아니라 입력된 매개 변수에 대 한 합니다.  
  
 에 대 한 호출 **SQLSetDescRec** 기본 전체 자릿수를 유도 하는 간격을 설정 하지만 값 (SQL_DESC_PRECISION 필드)에서 간격 초 전체 자릿수를 설정 합니다. 해당 *정밀도* 인수입니다.  
  
 지정 된 기본값 중 이전에 허용 되지 않는 응용 프로그램에 하는 경우 응용 프로그램 호출 하 여 SQL_DESC_PRECISION 또는 SQL_DESC_DATETIME_INTERVAL_PRECISION 필드를 설정 해야 **SQLSetDescField**합니다.  
  
 응용 프로그램을 호출 하는 경우 **SQLGetData** datetime 또는 간격 C 형식으로 데이터를 반환 하는 기본 간격 선행 자릿수 및 간격 초의 전체 자릿수가 사용 됩니다. 기본값을 적용할 수 있는 경우에 응용 프로그램 호출 해야 합니다 **SQLSetDescField** 설명자 필드 중 하나가 설정 또는 **SQLSetDescRec** SQL_DESC_PRECISION를 설정 하려면. 에 대 한 호출 **SQLGetData** 있어야를 *TargetType* 의 SQL_ARD_TYPE 설명자 필드에 값을 사용 하도록 합니다.  
  
 때 **SQLPutData** 라고, 호출에 대 한 APD 필드는 전체 자릿수 및 간격 초 실행 시 데이터 매개 변수 또는 열에 해당 하는 설명자 레코드의 필드에서 읽는 전체 자릿수를 유도 하는 간격 하 **SQLExecute** 또는 **SQLExecDirect**, 또는 필드에 대 한 호출 **SQLBulkOperations** 또는 **SQLSetPos**합니다.
