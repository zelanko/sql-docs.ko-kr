---
title: SQLBulkOperations로 행 페치 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], fetching rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: 0efee2d6-ce94-411e-9976-97ba28b8da37
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a99592210ff315db026d60b8743d4a3bca13c969
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061631"
---
# <a name="fetching-rows-with-sqlbulkoperations"></a>SQLBulkOperations로 행 페치
에를 호출 하 여 책갈피를 사용 하 여 행 집합에 데이터를 따라 다시 인출 될 수 있습니다 **SQLBulkOperations 합니다.** 인출할 행 바인딩된 책갈피 열 책갈피도 식별 됩니다. SQL_COLUMN_IGNORE 값을 사용 하 여 열 페치 하지 않은 합니다.  
  
 사용 하 여 대량 인출 하는 데 **SQLBulkOperations**, 응용 프로그램에서 다음을 수행 합니다.  
  
1.  검색 하 고 업데이트할 모든 행의 책갈피를 캐시 합니다. 둘 이상의 책갈피가 열 단위 바인딩을 사용 하 고 책갈피; 배열에 저장 됩니다. 둘 이상의 책갈피 행 단위 바인딩을 사용 하는 경우에 책갈피 행 구조의 배열에 저장 됩니다.  
  
2.  인출할 행 수 SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 설정 하 고 책갈피 또는 책갈피를 0 열에 배열을 포함 하는 버퍼를 바인딩합니다.  
  
3.  필요에 따라 각 열의 길이/표시기 버퍼의 값을 설정 합니다. 이 값은 이진 버퍼를 NULL로 설정할 열에 SQL_NULL_DATA를 바인딩된 열에 대 한 데이터의 바이트 길이 문자열 버퍼에 바인딩된 열에 대 한 데이터 또는 SQL_NTS 바이트 길이입니다. 응용 프로그램 (있는 경우) 해당 기본값으로 설정 된 열 또는 SQL_COLUMN_IGNORE NULL (하나, 없는 경우)의 길이/표시기 버퍼의 값을 설정 합니다.  
  
4.  호출 **SQLBulkOperations** 사용 하 여 합니다 *작업* 인수 SQL_FETCH_BY_BOOKMARK로 설정 합니다.  
  
 특정 열에서 수행할 작업을 방지 하기 위해 행 작업 배열을 사용 하 여 응용 프로그램에 대 한 않아도가 됩니다. 응용 프로그램이 바인딩된 책갈피 배열에만 해당 행에 대 한 책갈피를 복사 하 여 인출 하려는 행을 선택 합니다.
