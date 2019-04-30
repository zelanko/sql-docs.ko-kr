---
title: SQLSetPos 사용 하 여 행 집합의 행을 삭제 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], deleting rows
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
ms.assetid: 3117a47d-e179-4f76-89d0-656582f1c9bb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 78ee14838b467cfe6e555c97f1e74c65cccf98ff
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63049833"
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>SQLSetPos를 사용하여 행 집합에서 행 삭제
삭제 연산의 **SQLSetPos** 데이터 원본에서 테이블의 하나 이상의 선택한 행을 삭제 합니다. 사용 하 여 행을 삭제 하 **SQLSetPos**, 응용 프로그램이 호출 **SQLSetPos** 사용 하 여 *작업* SQL_DELETE로 설정 하 고 *RowNumber* 로 삭제할 행의 수입니다. 하는 경우 *RowNumber* 가 0 이면 행 집합의 모든 행이 삭제 됩니다.  
  
 이후에 **SQLSetPos** 반환 되 면 삭제 된 행에는 현재 행이 있으며 해당 상태는 sql_row_deleted가 됩니다. 행에 대 한 호출 등의 모든 추가 위치 지정된 작업에 사용할 수 없습니다 **SQLGetData** 하거나 **SQLSetPos**합니다.  
  
 행 집합의 모든 행을 삭제 하는 경우 (*RowNumber* 가 0), 응용 프로그램이 드라이버의 업데이트 작업과 동일한 방식으로 행 작업 배열을 사용 하 여 특정 행을 삭제 하지 못할 수 있습니다 **SQLSetPos** . (참조 [SQLSetPos를 사용 하 여 행 집합의 행 업데이트](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).)  
  
 삭제되는 모든 행은 결과 집합에 있는 행이여야 합니다. 응용 프로그램 버퍼를 인출 하 여 채워진 및 행 상태 배열이 유지 된 경우 이러한 각 행 위치에 해당 값은 SQL_ROW_DELETED, SQL_ROW_ERROR 또는 SQL_ROW_NOROW 되지 않습니다.
