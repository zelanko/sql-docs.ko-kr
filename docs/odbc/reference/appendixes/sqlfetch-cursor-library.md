---
title: SQLFetch (커서 라이브러리) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFetch function [ODBC], Cursor Library
ms.assetid: 35a0d493-778b-4fb1-84ee-a13540e2fe0e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2cb829f065421a13d3c7df06c670808bc3d9d77c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68064430"
---
# <a name="sqlfetch-cursor-library"></a>SQLFetch(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **Sqlfetch** 함수를 사용 하는 방법을 설명 합니다. **Sqlfetch**에 대 한 일반 정보는 [sqlfetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)를 참조 하세요.  
  
 커서 라이브러리를 사용 하는 경우 **Sqlfetch** 호출을 **sqlfetchscroll** 또는 **sqlextendedfetch**에 대 한 호출과 혼합할 수 없습니다.  
  
 SQL_ATTR_ROW_ARRAY_SIZE 값을 1 보다 큰 값으로 설정 하 여 **Sqlfetch** 를 호출 하면 커서 라이브러리는 드라이버에 대 한 호출을 전달 합니다. 드라이버가 ODBC 2 인 경우 *x* 드라이버, 행 집합 크기는 무시 되 고 **sqlfetch** 호출은 단일 데이터 행을 반환 합니다.  
  
 커서 라이브러리를 ODBC 2와 함께 사용 하는 경우입니다. *x* 드라이버는 **sqlfetch** 를 호출할 때 SQL_ATTR_ROW_BIND_OFFSET_PTR statement 특성에 의해 정의 된 바인딩 오프셋을 사용 하지 않습니다.  
  
 커서 라이브러리가 로드 되 면 응용 프로그램에서 **Sqlfetch** 를 호출 하 여 책갈피 열을 페치할 수 없습니다. 커서 라이브러리는를 통해 **Sqlfetch** 호출을 드라이버로 전달 하지만 책갈피를 사용 하도록 설정 하는 함수를 호출 하면 커서 라이브러리에서 책갈피 열을 가로챌 수 있습니다.
