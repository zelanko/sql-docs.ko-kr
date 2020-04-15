---
title: SQLSetPos를 통해 행 삭제 행 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 940bcc3e2ee6a042394797d6038028cce64862f1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305954"
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>SQLSetPos를 사용하여 행 집합에서 행 삭제
**SQLSetPos의** 삭제 작업을 수행하면 데이터 원본이 테이블의 선택된 행 중 하나 이상을 삭제합니다. **SQLSetPos를**사용 하 고 행을 삭제 하려면 응용 프로그램은 **sqlSetPos** *작업을* SQL_DELETE 설정 하 고 *RowNumber* 삭제 할 행의 수로 설정 합니다 호출 합니다. *RowNumber가* 0이면 행 집합의 모든 행이 삭제됩니다.  
  
 **SQLSetPos가** 반환되면 삭제된 행이 현재 행이며 해당 상태가 SQL_ROW_DELETED. 이 행은 **SQLGetData** 또는 **SQLSetPos**에 대한 호출과 같은 추가 위치에 있는 작업에서는 사용할 수 없습니다.  
  
 행 집합의 모든 행을 삭제하는 경우 *(RowNumber는* 0과 같음) 응용 프로그램은 **SQLSetPos의**업데이트 작업과 같은 방식으로 행 작업 배열을 사용하여 드라이버가 특정 행을 삭제하지 못하게 할 수 있습니다. [(SQLSetPos를 가진 행 업데이트 참조).](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
 삭제되는 모든 행은 결과 집합에 있는 행이여야 합니다. 응용 프로그램 버퍼가 가져오기로 채워지고 행 상태 배열이 유지된 경우 이러한 각 행 위치의 해당 값은 SQL_ROW_DELETED, SQL_ROW_ERROR 또는 SQL_ROW_NOROW 않아야 합니다.
