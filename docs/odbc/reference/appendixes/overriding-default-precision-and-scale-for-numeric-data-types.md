---
title: 숫자 데이터 형식에 대 한 기본 전체 자릿수 및 소수 자릿수 재정의 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303594"
---
# <a name="overriding-default-precision-and-scale-for-numeric-data-types"></a>숫자 데이터 형식에 대한 기본 전체 자릿수 및 소수 자릿수 재정의
**SQLBindCol** 또는 SQLSetDescField를 호출 하 여 **SQLSetDescField**의 SQL_DESC_TYPE 필드가 SQL_C_NUMERIC로 설정 된 경우, 나의 SQL_DESC_SCALE 필드는 0으로 설정 되 고 SQL_DESC_PRECISION 필드는 드라이버 정의 기본 전체 자릿수로 설정 됩니다. **SQLBindParameter** 또는 **SQLSetDescField**를 호출 하 여 apd의 SQL_DESC_TYPE 필드가 SQL_C_NUMERIC으로 설정 된 경우에도 마찬가지입니다. 입력, 입/출력 또는 출력 매개 변수의 경우에도 마찬가지입니다.  
  
 이전에 설명한 기본값 중 하나를 응용 프로그램에 사용할 수 없는 경우 응용 프로그램은 **SQLSetDescField** 또는 **SQLSetDescRec**를 호출 하 여 SQL_DESC_SCALE 또는 SQL_DESC_PRECISION 필드를 설정 해야 합니다.  
  
 응용 프로그램이 **SQLGetData** 를 호출 하 여 데이터를 SQL_C_NUMERIC 구조체로 반환 하는 경우 기본 SQL_DESC_SCALE 및 SQL_DESC_PRECISION 필드가 사용 됩니다. 기본값을 사용할 수 없는 경우 응용 프로그램에서 **SQLSetDescRec** 또는 **SQLSetDescField** 를 호출 하 여 필드를 설정한 다음, SQL_ARD_TYPE *TargetType* 과 함께 **SQLGetData** 를 호출 하 여 설명자 필드의 값을 사용 해야 합니다.  
  
 **Sqlputdata** 가 호출 되 면 호출은 **Sqlexecute** 또는 **sqlputdata**에 대 한 호출에 대 한 Apd 필드 또는 **SQLBulkOperations** 또는 **SQLSetPos**호출의 필드를 사용 하 여 실행 시 데이터 매개 변수 또는 열에 해당 하는 설명자 레코드의 SQL_DESC_SCALE 및 SQL_DESC_PRECISION 필드를 사용 합니다.
