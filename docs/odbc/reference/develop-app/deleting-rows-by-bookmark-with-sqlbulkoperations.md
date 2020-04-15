---
title: SQLBulkOperations를 통해 책갈피로 행 삭제 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305964"
---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>SQLBulkOperations로 책갈피별로 행 삭제
책갈피별로 행을 삭제할 때 **SQLBulkOperations는** 데이터 원본이 테이블의 하나 이상의 선택된 행을 삭제하도록 합니다. 행은 바인딩된 책갈피 열의 책갈피로 식별됩니다.  
  
 **SQLBulkOperations를**사용하여 책갈피로 행을 삭제하려면 응용 프로그램은 다음을 수행합니다.  
  
1.  삭제할 모든 행의 책갈피를 검색하고 캐시합니다. 두 개 이상의 책갈피와 열별 바인딩이 사용되는 경우 책갈피는 배열에 저장됩니다. 책갈피와 행별 바인딩이 두 개 이상 사용되는 경우 책갈피는 행 구조의 배열에 저장됩니다.  
  
2.  SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 책갈피 수로 설정하고 책갈피 값 또는 책갈피 배열을 포함하는 버퍼를 열 0에 바인딩합니다.  
  
3.  *작업을* SQL_DELETE_BY_BOOKMARK 설정된 **SQLBulkOperations을** 호출합니다.
