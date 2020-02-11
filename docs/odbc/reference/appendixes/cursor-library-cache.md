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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019066"
---
# <a name="cursor-library-cache"></a>커서 라이브러리 캐시
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 커서 라이브러리는 결과 집합의 각 데이터 행에 대해 바인딩된 각 열에 대 한 데이터, 각 바인딩된 열의 데이터 길이 및 행의 상태를 캐시 합니다. 커서 라이브러리는 캐시의 값을 모두 사용 하 여 **Sqlfetch** 및 **sqlfetchscroll** 을 통해 반환 하 고, 배치 된 작업에 대해 검색 된 문을 생성 합니다. 자세한 내용은 [검색 문 생성](../../../odbc/reference/appendixes/constructing-searched-statements.md)을 참조 하세요.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [열 데이터](../../../odbc/reference/appendixes/column-data.md)  
  
-   [열 데이터의 길이](../../../odbc/reference/appendixes/length-of-column-data.md)  
  
-   [행 상태](../../../odbc/reference/appendixes/row-status.md)  
  
-   [캐시의 위치](../../../odbc/reference/appendixes/location-of-cache.md)
