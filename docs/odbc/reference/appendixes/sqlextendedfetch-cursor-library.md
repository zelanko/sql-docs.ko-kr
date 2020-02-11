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
ms.openlocfilehash: a3fd7d02d74b0e19d91871c5df7c9c5915d028f5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68064449"
---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **Sqlextendedfetch** 함수를 사용 하는 방법을 설명 합니다. **Sqlextendedfetch**에 대 한 일반 정보는 [Sqlextendedfetch 함수](../../../odbc/reference/syntax/sqlextendedfetch-function.md)를 참조 하세요.  
  
 커서 라이브러리는 드라이버에서 **Sqlfetch** 를 반복 해 서 호출 하 여 **sqlextendedfetch** 를 구현 합니다.  
  
 커서 라이브러리는 SQL_FETCH_BOOKMARK의 *Fetchorientation* 로 **sqlextendedfetch** 호출을 지원 합니다.  
  
 커서 라이브러리를 사용 하는 경우 **Sqlextendedfetch** 에 대 한 호출은 **sqlextendedfetch** 또는 **sqlfetch**호출을 혼합할 수 없습니다.
