---
title: 구현 참고 사항 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7ec14b9c-69b8-4c6e-838a-88d1ebdc8725
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a47c292695eb1f68700eefac1aa63732e8606f26
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188939"
---
# <a name="implementation-notes"></a>구현 참고
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 섹션에서는 ODBC 커서 라이브러리 구현 되는 방식을 설명 합니다. 커서 라이브러리를 해당 캐시를 유지 관리, SQL 문을 실행 및 ODBC 함수를 구현 하는 방법을 설명 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [커서 라이브러리 캐시](../../../odbc/reference/appendixes/cursor-library-cache.md)  
  
-   [SQL 문 처리](../../../odbc/reference/appendixes/processing-sql-statements.md)  
  
-   [ODBC 함수 및 커서 라이브러리](../../../odbc/reference/appendixes/odbc-functions-and-the-cursor-library.md)
