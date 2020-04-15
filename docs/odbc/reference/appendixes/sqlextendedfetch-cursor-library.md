---
title: SQLExtendedFetch (커서 라이브러리) | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe39b2d2cbbaf72ce3844c35187040589d1dac58
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302064"
---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLExtendedFetch** 함수의 사용에 대해 설명합니다. **SQLExtendedFetch에**대한 일반 정보는 [SQLExtendedFetch 함수를](../../../odbc/reference/syntax/sqlextendedfetch-function.md)참조하십시오.  
  
 커서 라이브러리는 드라이버에서 **SQLFetch를** 반복적으로 호출하여 **SQLExtendedFetch를** 구현합니다.  
  
 커서 라이브러리는 SQL_FETCH_BOOKMARK *FetchOrientation를* 사용하여 **SQLExtendedFetch** 호출을 지원합니다.  
  
 커서 라이브러리를 사용하는 경우 **SQLExtendedFetch에** 대한 호출을 **SQLFetchScroll** 또는 **SQLFetch**에 대한 호출과 혼합할 수 없습니다.
