---
title: "커서 라이브러리 캐시 | Microsoft Docs"
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
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: d6a91cd6-3905-4e3a-98ab-37fce893dbe1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 06b893a857f87c2d6c3911e3d81fd0cd02d89668
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="cursor-library-cache"></a>커서 라이브러리 캐시
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 각 결과 집합의 데이터 행에 대 한 커서 라이브러리는 바인딩된 각 열에 있는 데이터의 길이 행의 상태 바인딩된 각 열에 대 한 데이터를 캐시합니다. 커서 라이브러리를 사용 하 여 값 모두 캐시에 통한 반환할 **SQLFetch** 및 **SQLFetchScroll** 위치 지정된 작업에 대 한 검색 결과 문을 생성 하 고 있습니다. 자세한 내용은 참조 [검색 문을 생성](../../../odbc/reference/appendixes/constructing-searched-statements.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [열 데이터](../../../odbc/reference/appendixes/column-data.md)  
  
-   [열 데이터의 길이](../../../odbc/reference/appendixes/length-of-column-data.md)  
  
-   [행 상태](../../../odbc/reference/appendixes/row-status.md)  
  
-   [캐시의 위치](../../../odbc/reference/appendixes/location-of-cache.md)

