---
title: SQL 문 처리 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
ms.assetid: 54dad6a3-e86c-477b-ba7c-4e95e0385ec1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3b41656bf637c2a83d366ac28e505ff0a0475ff
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="processing-sql-statements"></a>SQL 문 처리
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 ODBC 커서 라이브러리는 다음을 제외한 드라이버를 직접 모든 SQL 문에 전달합니다.  
  
-   배치 update 및 delete 문  
  
-   **업데이트에 대 한 선택** 문  
  
-   일괄 처리 된 SQL 문  
  
 실행 위치 지정된 update 및 delete 문을를 호출 하는 행에 커서를 배치 **SQLGetData** 해당 행에 대 한 커서 라이브러리는 행을 식별 하는 검색 된 문을 생성 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [위치 지정 업데이트 및 Delete 문 처리](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)  
  
-   [SELECT FOR UPDATE 문 처리](../../../odbc/reference/appendixes/processing-select-for-update-statements.md)  
  
-   [SQL 문의 일괄 처리](../../../odbc/reference/appendixes/processing-batches-of-sql-statements.md)  
  
-   [검색된 문 생성](../../../odbc/reference/appendixes/constructing-searched-statements.md)
