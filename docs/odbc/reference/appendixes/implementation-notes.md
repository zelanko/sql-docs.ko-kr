---
title: 구현 노트 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7ec14b9c-69b8-4c6e-838a-88d1ebdc8725
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 970188a2fca45706405e398cece0f04d38dfdc68
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284314"
---
# <a name="implementation-notes"></a>구현 참고 사항
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 이 섹션에서는 ODBC 커서 라이브러리가 구현되는 방법에 대해 설명합니다. 커서 라이브러리가 캐시를 유지 관리하고 SQL 문을 실행하고 ODBC 함수를 구현하는 방법을 설명합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [커서 라이브러리 캐시](../../../odbc/reference/appendixes/cursor-library-cache.md)  
  
-   [SQL 문 처리](../../../odbc/reference/appendixes/processing-sql-statements.md)  
  
-   [ODBC 함수 및 커서 라이브러리](../../../odbc/reference/appendixes/odbc-functions-and-the-cursor-library.md)
