---
title: SQLFreeStmt (커서 라이브러리) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeStmt function [ODBC], Cursor Library
ms.assetid: 47bfbd4d-9453-4609-958d-1e05794cb223
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d78075593926c15dbaeb1904603b08e990f64983
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302024"
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLFreeStmt** 함수를 사용 하는 방법을 설명 합니다. **SQLFreeStmt**에 대 한 일반 정보는 [SQLFreeStmt 함수](../../../odbc/reference/syntax/sqlfreestmt-function.md)를 참조 하세요.  
  
 응용 프로그램이 **Sqlextendedfetch**, **Sqlfetch**또는 **sqlextendedfetch**을 호출한 후 SQL_UNBIND 옵션을 사용 하 여 **SQLFreeStmt** 를 호출 하면 커서 라이브러리에서 오류를 반환 합니다. 응용 프로그램은 결과 집합 열을 바인딩 해제 하기 전에 SQL_CLOSE 옵션을 사용 하 여 **SQLCloseCursor** 또는 **SQLFreeStmt** 를 호출 해야 합니다.
