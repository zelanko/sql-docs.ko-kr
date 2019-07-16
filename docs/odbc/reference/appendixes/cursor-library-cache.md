---
title: 커서 라이브러리 캐시 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: d6a91cd6-3905-4e3a-98ab-37fce893dbe1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 597abe268979852d754e2e3e86ae81daa8f3fed8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019066"
---
# <a name="cursor-library-cache"></a>커서 라이브러리 캐시
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 결과 집합에는 데이터의 각 행에 대해 커서 라이브러리는 각 바인딩된 열에 바인딩된 각 열에 있는 데이터의 길이 행의 상태에 대 한 데이터를 캐시합니다. 커서 라이브러리를 통해 반환할 모두 캐시에 값을 사용 해도 **SQLFetch** 하 고 **SQLFetchScroll** 및 위치 지정된 작업에 대 한 검색된 문을 생성 합니다. 자세한 내용은 [검색 문을 생성](../../../odbc/reference/appendixes/constructing-searched-statements.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [열 데이터](../../../odbc/reference/appendixes/column-data.md)  
  
-   [열 데이터의 길이](../../../odbc/reference/appendixes/length-of-column-data.md)  
  
-   [행 상태](../../../odbc/reference/appendixes/row-status.md)  
  
-   [캐시의 위치](../../../odbc/reference/appendixes/location-of-cache.md)
