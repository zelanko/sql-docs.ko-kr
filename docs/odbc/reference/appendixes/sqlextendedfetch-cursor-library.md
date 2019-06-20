---
title: SQLExtendedFetch (커서 라이브러리) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Cursor Library
ms.assetid: 06fbf06f-127b-475c-b636-7b784918475d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 600d90c14ae8b08a4860f3cff49c1615a9587063
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199538"
---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는의 사용을 설명 합니다 **SQLExtendedFetch** 커서 라이브러리의 함수입니다. 에 대 한 일반 정보에 대 한 **SQLExtendedFetch**를 참조 하십시오 [SQLExtendedFetch 함수](../../../odbc/reference/syntax/sqlextendedfetch-function.md)합니다.  
  
 커서 라이브러리 구현 **SQLExtendedFetch** 반복적으로 호출 하 여 **SQLFetch** 드라이버에서입니다.  
  
 커서 라이브러리 호출을 지 원하는 **SQLExtendedFetch** 사용 하 여를 *FetchOrientation* 에서는 SQL_FETCH_BOOKMARK의 합니다.  
  
 커서 라이브러리를 사용 하는 경우 호출 **SQLExtendedFetch** 중 하나를 호출 하 여 혼합할 수 없습니다 **SQLFetchScroll** 하거나 **SQLFetch**합니다.
