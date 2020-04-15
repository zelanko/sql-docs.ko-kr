---
title: SQLSet스크롤 옵션 (커서 라이브러리) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Cursor Library
ms.assetid: c5c0ac6d-a6c1-4077-8186-1644df1944f8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0099ca5e9bcb3aefdd86e0132f52d110ab64e8a4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304914"
---
# <a name="sqlsetscrolloptions-cursor-library"></a>SQLSetScrollOptions(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLSetScrollOptions** 함수의 사용에 대해 설명합니다. **SQLSetScroll옵션에**대한 일반적인 정보는 [SQLSetScrollOptions 함수를](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)참조하십시오.  
  
 커서 라이브러리는 이전 버전과의 호환성에 대해서만 **SQLSetScrollOptions를** 지원합니다. 응용 프로그램은 SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE 및 SQL_ATTR_ROW_ARRAY_SIZE 명령문 특성을 대신 사용해야 합니다.
