---
title: SQLGetStmtAttr (커서 라이브러리) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtAttr function [ODBC], Cursor Library
ms.assetid: 6c34e1ef-4273-4afb-a7d3-f9017ab69c5e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9b29d21c166751f5a57b7951cb6c028861cb501
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87362953"
---
# <a name="sqlgetstmtattr-cursor-library"></a>SQLGetStmtAttr(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLGetStmtAttr** 함수를 사용 하는 방법을 설명 합니다. **SQLGetStmtAttr**에 대 한 일반 정보는 [SQLGetStmtAttr 함수](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)를 참조 하세요.  
  
 커서 라이브러리는 **SQLGetStmtAttr**을 사용 하는 다음과 같은 문 특성을 지원 합니다.  

:::row:::
    :::column:::
        SQL_ATTR_CONCURRENCY  
        SQL_ATTR_CURSOR_TYPE  
        SQL_ATTR_FETCH_BOOKMARK_PTR  
        SQL_ATTR_PARAM_BIND_OFFSET_PTR  
        SQL_ATTR_PARAM_BIND_TYPE  
    :::column-end:::
    :::column:::
        SQL_ATTR_ROW_ARRAY_SIZE  
        SQL_ATTR_ROW_BIND_OFFSET_PTR  
        SQL_ATTR_ROW_BIND_TYPE  
        SQL_ATTR_ROW_NUMBER  
        SQL_ATTR_SIMULATE_CURSOR  
    :::column-end:::
:::row-end:::
