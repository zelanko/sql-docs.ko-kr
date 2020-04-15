---
title: SQLFreeStmt (커서 라이브러리) | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302024"
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLFreeStmt** 함수의 사용에 대해 설명합니다. **SQLFreeStmt에**대한 일반 정보는 [SQLFreeStmt 함수를](../../../odbc/reference/syntax/sqlfreestmt-function.md)참조하십시오.  
  
 응용 프로그램이 **SQLExtendedFetch,** **SQLFetch**또는 **SQLFetch스크롤을**호출한 후 SQL_UNBIND 옵션을 사용 하 여 **SQLFreeStmt를** 호출 하는 경우 커서 라이브러리오류를 반환 합니다. 결과 집합 열을 바인딩 해제하려면 먼저 응용 프로그램에서 **SQLCloseCursor** 또는 **SQLFreeStmt를** SQL_CLOSE 옵션으로 호출해야 합니다.
