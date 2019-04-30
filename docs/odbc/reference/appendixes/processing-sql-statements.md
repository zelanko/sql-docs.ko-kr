---
title: SQL 문 처리 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
ms.assetid: 54dad6a3-e86c-477b-ba7c-4e95e0385ec1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d5aa94062f90154126fb18c3658adb39bb1d5c0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63057055"
---
# <a name="processing-sql-statements"></a>SQL 문 처리
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 모든 SQL 문에 다음을 제외한 드라이버에 직접 전달 하는 ODBC 커서 라이브러리:  
  
-   배치 업데이트 및 delete 문  
  
-   **SELECT FOR UPDATE** 문  
  
-   일괄 처리 된 SQL 문  
  
 실행 위치 지정된 update 및 delete 문을를 호출 하는 행에 커서를 놓고 **SQLGetData** 해당 행에 대 한 커서 라이브러리는 행 식별 하는 검색된 문을 생성 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [위치 지정 업데이트 및 Delete 문 처리](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)  
  
-   [SELECT FOR UPDATE 문 처리](../../../odbc/reference/appendixes/processing-select-for-update-statements.md)  
  
-   [SQL 문의 일괄 처리](../../../odbc/reference/appendixes/processing-batches-of-sql-statements.md)  
  
-   [검색된 문 생성](../../../odbc/reference/appendixes/constructing-searched-statements.md)
