---
description: SQLSetPos를 사용하여 행 집합에서 행 삭제
title: SQLSetPos를 사용 하 여 행 집합의 행 삭제 Microsoft Docs
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
ms.openlocfilehash: 42b61aa9af15526420b6f2d4ef7e8c945e0da105
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476775"
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>SQLSetPos를 사용하여 행 집합에서 행 삭제
**SQLSetPos** 의 삭제 작업은 데이터 원본에서 하나 이상의 선택 된 테이블 행을 삭제 합니다. **Sqlsetpos**를 사용 하 여 행을 삭제 하기 위해 응용 프로그램은 *작업* 을 SQL_DELETE로 설정 하 고 *RowNumber* 를 삭제할 행 번호로 설정 하 여 **SQLSetPos** 를 호출 합니다. *RowNumber* 가 0 이면 행 집합의 모든 행이 삭제 됩니다.  
  
 **SQLSetPos** 가 반환 된 후 삭제 된 행은 현재 행 이며 상태는 SQL_ROW_DELETED입니다. **SQLGetData** 또는 **SQLSetPos**호출 등의 추가 위치 작업에서 행을 사용할 수 없습니다.  
  
 행 집합의 모든 행을 삭제 하는 경우 (*RowNumber* 가 0 인 경우) 응용 프로그램은 **SQLSetPos**의 업데이트 작업과 동일한 방식으로 행 작업 배열을 사용 하 여 드라이버가 특정 행을 삭제 하지 못하도록 할 수 있습니다. ( [SQLSetPos를 사용 하 여 행 집합의 행 업데이트](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)참조)  
  
 삭제되는 모든 행은 결과 집합에 있는 행이여야 합니다. 페치를 통해 응용 프로그램 버퍼를 채우고 행 상태 배열이 유지 된 경우 이러한 각 행 위치에 있는 값을 SQL_ROW_DELETED, SQL_ROW_ERROR 또는 SQL_ROW_NOROW 하지 않아야 합니다.
