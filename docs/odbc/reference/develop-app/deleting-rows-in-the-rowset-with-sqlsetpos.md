---
title: SQLSetPos이 있는 행 집합의 행 삭제 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], deleting rows
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
ms.assetid: 3117a47d-e179-4f76-89d0-656582f1c9bb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 60d225926a6c11ac81ae8fe6fea8935ee88f1778
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>SQLSetPos이 있는 행 집합의 행 삭제
삭제 작업의 **SQLSetPos** 은 데이터 원본 테이블의 하나 이상의 선택 된 행을 삭제 합니다. 행을 삭제 하려면 **SQLSetPos**, 응용 프로그램 호출 **SQLSetPos** 와 *작업* SQL_DELETE로 설정 하 고 *RowNumber* 로 설정는 삭제할 행의 수입니다. 경우 *RowNumber* 가 0 이면 행 집합의 모든 행이 삭제 됩니다.  
  
 후 **SQLSetPos** 삭제 된 행이 현재 행 및 해당 상태는 sql_row_deleted가 반환 됩니다. 행에 대 한 호출 등의 추가 위치 지정 작업에서 사용할 수 없습니다 **SQLGetData** 또는 **SQLSetPos**합니다.  
  
 행 집합의 모든 행을 삭제할 때 (*RowNumber* 가 0), 응용 프로그램이 드라이버의 업데이트 작업의 경우와 마찬가지로 행 작업 배열을 사용 하 여 특정 행을 삭제 하지 못할 수 있습니다 **SQLSetPos** . (참조 [SQLSetPos와 행 집합의 행이 업데이트](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).)  
  
 삭제되는 모든 행은 결과 집합에 있는 행이여야 합니다. 응용 프로그램 버퍼를 인출 하 여 기록한 및 행 상태 배열이 유지 된 경우 이러한 각 행 위치에서 값을은 SQL_ROW_DELETED, SQL_ROW_ERROR 또는 SQL_ROW_NOROW 안 됩니다.
