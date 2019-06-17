---
title: SQLBulkOperations로 책갈피 별로 행 삭제 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5895a106c389afe2d1979cf8d9c16e92f570538a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63049946"
---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>SQLBulkOperations로 책갈피별로 행 삭제
책갈피에서 행을 삭제할 때 **SQLBulkOperations** 데이터 원본에서 테이블의 하나 이상의 선택한 행을 삭제 합니다. 행 바인딩된 책갈피 열에 책갈피를 통해 식별 됩니다.  
  
 로 책갈피 별로 행 삭제 **SQLBulkOperations**, 응용 프로그램에서 다음을 수행 합니다.  
  
1.  검색 하 고 삭제할 모든 행의 책갈피를 캐시 합니다. 둘 이상의 책갈피가 열 단위 바인딩을 사용 하 고 책갈피; 배열에 저장 됩니다. 둘 이상의 책갈피 행 단위 바인딩을 사용 하는 경우에 책갈피 행 구조의 배열에 저장 됩니다.  
  
2.  책갈피의 수 SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 설정 하 고 책갈피 또는 책갈피를 0 열에 배열을 포함 하는 버퍼를 바인딩합니다.  
  
3.  호출 **SQLBulkOperations** 사용 하 여 *작업* SQL_DELETE_BY_BOOKMARK로 설정 합니다.
