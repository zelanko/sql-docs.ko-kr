---
title: SQLSetScrollOptions (커서 라이브러리) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 18a0bc111f6b4e8d82d0ed353837b499f920479e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68023365"
---
# <a name="sqlsetscrolloptions-cursor-library"></a>SQLSetScrollOptions(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLSetScrollOptions** 함수를 사용 하는 방법을 설명 합니다. **SQLSetScrollOptions**에 대 한 일반 정보는 [SQLSetScrollOptions 함수](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)를 참조 하세요.  
  
 커서 라이브러리는 이전 버전과의 호환성을 위해서만 **SQLSetScrollOptions** 을 지원 합니다. 응용 프로그램은 SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE 및 SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 대신 사용 해야 합니다.
