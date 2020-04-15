---
title: SQLBulkOperations로 행 가져오기 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae0b4c2114059cecaaf8f8825169300f131bd473
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305652"
---
# <a name="fetching-rows-with-sqlbulkoperations"></a>SQLBulkOperations로 행 페치
**SQLBulkOperations에** 대한 호출을 통해 책갈피를 사용하여 데이터를 행 집합으로 다시 가져올 수 있습니다. 가져올 행은 바인딩된 책갈피 열의 책갈피로 식별됩니다. SQL_COLUMN_IGNORE 값이 있는 열은 가져오지 않습니다.  
  
 **SQLBulkOperations를**사용하여 대량 인출을 수행하려면 응용 프로그램이 다음을 수행합니다.  
  
1.  업데이트할 모든 행의 책갈피를 검색하고 캐시합니다. 두 개 이상의 책갈피와 열별 바인딩이 사용되는 경우 책갈피는 배열에 저장됩니다. 책갈피와 행별 바인딩이 두 개 이상 사용되는 경우 책갈피는 행 구조의 배열에 저장됩니다.  
  
2.  SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 가져올 행 수로 설정하고 책갈피 값 또는 책갈피 배열을 포함하는 버퍼를 열 0으로 바인딩합니다.  
  
3.  필요에 따라 각 열의 길이/표시기 버퍼의 값을 설정합니다. 문자열 버퍼에 바인딩된 열에 대한 데이터 또는 SQL_NTS 바이트 길이, 이진 버퍼에 바인딩된 열에 대한 데이터의 바이트 길이 및 NULL로 설정될 모든 열에 대한 SQL_NULL_DATA. 응용 프로그램은 SQL_COLUMN_IGNORE 위해 기본값(있는 경우) 또는 NULL(그렇지 않은 경우)으로 설정될 해당 열의 길이/표시기 버퍼에서 값을 설정합니다.  
  
4.  SQL_FETCH_BY_BOOKMARK 설정된 *작업* 인수를 사용하여 **SQLBulkOperations를** 호출합니다.  
  
 응용 프로그램이 특정 열에서 수행되는 작업을 방지하기 위해 행 작업 배열을 사용할 필요가 없습니다. 응용 프로그램은 해당 행의 책갈피만 바인딩된 책갈피 배열에 복사하여 가져올 행을 선택합니다.
