---
title: "SQLFetch (커서 라이브러리) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLFetch function [ODBC], Cursor Library
ms.assetid: 35a0d493-778b-4fb1-84ee-a13540e2fe0e
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1e5cabca53c503e2cd0c12147248b11da84ed157
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlfetch-cursor-library"></a>SQLFetch (커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목의 사용을 설명는 **SQLFetch** 커서 라이브러리의 함수가 있습니다. 에 대 한 일반적인 내용은 **SQLFetch**, 참조 [SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)합니다.  
  
 커서 라이브러리를 사용 하는 경우에 대 한 호출이 **SQLFetch** 에 대 한 호출 함께 **SQLFetchScroll** 또는 **SQLExtendedFetch**합니다.  
  
 경우 **SQLFetch** 라고 커서 라이브러리와 SQL_ATTR_ROW_ARRAY_SIZE가 1 보다 큰 값으로 설정, 드라이버에 대 한 호출을 전달 합니다. 드라이버는 ODBC 2 하는 경우. *x* 드라이버를 행 집합 크기는 무시 됩니다에 대 한 호출은 **SQLFetch** 데이터의 단일 행을 반환 합니다.  
  
 커서 라이브러리는 ODBC 2 함께 사용 됩니다. *x* 드라이버가, 오프셋 (SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성에 의해 정의 됨) 바인딩 않습니다 때 사용 **SQLFetch** 호출 됩니다.  
  
 응용 프로그램을 호출할 수 없습니다 커서 라이브러리를 로드할 때 **SQLFetch** 책갈피 열 가져옵니다. 커서 라이브러리 호출이 전달 **SQLFetch** 통해 드라이버 하지만 함수에 책갈피를 사용 하도록 설정 하 고 바인딩할 책갈피 열에 대 한 호출에서 차단 되어 커서 라이브러리입니다.

