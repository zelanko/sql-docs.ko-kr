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
manager: craigg
ms.openlocfilehash: e1fe6765c0ff8a057aac8e86ea5ad4aa1ac388b4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47739671"
---
# <a name="sqlsetscrolloptions-cursor-library"></a>SQLSetScrollOptions(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는의 사용을 설명 합니다 **SQLSetScrollOptions** 커서 라이브러리의 함수입니다. 에 대 한 일반 정보에 대 한 **SQLSetScrollOptions**를 참조 하십시오 [SQLSetScrollOptions 함수](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)합니다.  
  
 커서 라이브러리 지원 **SQLSetScrollOptions** ; 이전 버전과 호환성을 위해서만 응용 프로그램 해야 SQL_ATTR_CURSOR_TYPE, SQL_ATTR_CONCURRENCY를 SQL_ATTR_ROW_ARRAY_SIZE 문 특성을 사용 합니다.
