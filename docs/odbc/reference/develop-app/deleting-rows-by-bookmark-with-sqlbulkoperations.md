---
title: SQLBulkOperations로 책갈피를 사용 하 여 행 삭제 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], SQLBulkOperations
- SQLBulkOperations function [ODBC], deleting rows
- updating data [ODBC], SQLBulkOperations
ms.assetid: 46139ec9-7095-481a-bf45-20200a2fdc03
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6b6a4c1b24ee276c86175392eb45ac5ce0aa45e5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305964"
---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>SQLBulkOperations로 책갈피별로 행 삭제
책갈피를 사용 하 여 행을 삭제 하는 경우 **SQLBulkOperations** 는 데이터 원본이 테이블에서 하나 이상의 선택 된 행을 삭제 하도록 합니다. 행은 바인딩된 책갈피 열의 책갈피에 의해 식별 됩니다.  
  
 **SQLBulkOperations**로 책갈피를 사용 하 여 행을 삭제 하려면 응용 프로그램에서 다음을 수행 합니다.  
  
1.  삭제할 모든 행의 책갈피를 검색 하 고 캐시 합니다. 책갈피와 열 단위 바인딩이 모두 사용 되는 경우 책갈피는 배열에 저장 됩니다. 책갈피와 행 단위 바인딩이 모두 사용 되는 경우 책갈피는 행 구조의 배열에 저장 됩니다.  
  
2.  SQL_ATTR_ROW_ARRAY_SIZE statement 특성을 책갈피의 개수로 설정 하 고 책갈피 값 또는 책갈피의 배열을 포함 하는 버퍼를 열 0에 바인딩합니다.  
  
3.  *작업이* SQL_DELETE_BY_BOOKMARK로 설정 된 **SQLBulkOperations** 를 호출 합니다.
