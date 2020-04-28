---
title: Interval 데이터 형식에 대 한 선행 및 초 전체 자릿수 재정의 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303604"
---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>간격 데이터 형식에 대한 기본 선행 및 초 전체 자릿수 재정의
**SQLBindCol** 또는 SQLSetDescField를 호출 하 여 **SQLSetDescField**의 SQL_DESC_TYPE 필드가 datetime 또는 interval C 형식으로 설정 된 경우 간격 (초)의 전체 자릿수가 포함 된 SQL_DESC_PRECISION 필드가 다음 기본값으로 설정 됩니다.  
  
-   6 타임 스탬프 및 모든 interval 데이터 형식 (두 번째 구성 요소 포함)  
  
-   다른 모든 데이터 형식의 경우 0입니다.  
  
 모든 interval 데이터 형식에 대해 간격 선행 필드 전체 자릿수를 포함 하는 SQL_DESC_DATETIME_INTERVAL_PRECISION 설명자 필드는 기본값 2로 설정 됩니다.  
  
 **SQLBindParameter** 또는 **SQLSetDescField**를 호출 하 여 apd의 SQL_DESC_TYPE 필드가 datetime 또는 interval C 형식으로 설정 된 경우 apd의 SQL_DESC_PRECISION 및 SQL_DESC_DATETIME_INTERVAL_PRECISION 필드는 이전에 지정 된 기본값으로 설정 됩니다. 입력 매개 변수의 경우에는 true이 고 입력/출력 또는 출력 매개 변수는 그렇지 않습니다.  
  
 **SQLSetDescRec** 에 대 한 호출은 interval 선행 전체 자릿수를 기본값으로 설정 하지만 SQL_DESC_PRECISION 필드에서 간격 초 전체 자릿수를 *전체 자릿수* 인수 값으로 설정 합니다.  
  
 이전에 지정 된 기본값 중 하나가 응용 프로그램에 허용 되지 않는 경우 응용 프로그램은 **SQLSetDescField**를 호출 하 여 SQL_DESC_PRECISION 또는 SQL_DESC_DATETIME_INTERVAL_PRECISION 필드를 설정 해야 합니다.  
  
 응용 프로그램이 **SQLGetData** 를 호출 하 여 datetime 또는 interval C 형식으로 데이터를 반환 하는 경우 기본 interval 선행 전체 자릿수 및 간격 (초)의 전체 자릿수가 사용 됩니다. 기본값을 사용할 수 없는 경우 응용 프로그램은 **SQLSetDescField** 를 호출 하 여 설명자 필드를 설정 하거나 **SQLSetDescRec** 를 설정 하 여 SQL_DESC_PRECISION를 설정 해야 합니다. **SQLGetData** 호출에는 설명자 필드의 값을 사용 하는 SQL_ARD_TYPE의 *TargetType* 이 있어야 합니다.  
  
 **Sqlputdata** 를 호출 하는 경우에는 실행 시 데이터 매개 변수 또는 열에 해당 하는 설명자 레코드의 필드에서 ( **Sqlexecute** 또는 **sqlputdata**에 대 한 호출에 대 한 Apd 필드 또는 **SQLBulkOperations** 또는 **SQLSetPos**호출에 대 한 호출에 대 한 필드)에서 간격 선행 전체 자릿수 및 간격 (초)의 전체 자릿수를 읽습니다.
