---
title: SQLGetStmtAttr (커서 라이브러리) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLGetStmtAttr function [ODBC], Cursor Library
ms.assetid: 6c34e1ef-4273-4afb-a7d3-f9017ab69c5e
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8ee808461c077eb1ea735ccc8aef6de1b843f723
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetstmtattr-cursor-library"></a>SQLGetStmtAttr (커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목의 사용을 설명는 **SQLGetStmtAttr** 커서 라이브러리의 함수가 있습니다. 에 대 한 일반적인 내용은 **SQLGetStmtAttr**, 참조 [SQLGetStmtAttr 함수](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)합니다.  
  
 커서 라이브러리는 다음 문 특성과 지원 **SQLGetStmtAttr**:  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROW_NUMBER|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_ROW_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_SIMULATE_CURSOR|
