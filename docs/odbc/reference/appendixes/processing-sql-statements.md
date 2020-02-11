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
ms.openlocfilehash: d9452ade90f6967dff6d72d5692efcf91b93154d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68057237"
---
# <a name="processing-sql-statements"></a>SQL 문 처리
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 ODBC 커서 라이브러리는 다음을 제외 하 고 모든 SQL 문을 드라이버에 직접 전달 합니다.  
  
-   위치 지정 update 및 delete 문  
  
-   **SELECT FOR UPDATE** 문  
  
-   일괄 처리 된 SQL 문  
  
 위치 지정 update 및 delete 문을 실행 하 고 행에 커서를 배치 하 여 해당 행에 대 한 **SQLGetData** 를 호출 하려면 커서 라이브러리에서 행을 식별 하는 검색 문을 생성 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [위치 지정 업데이트 및 Delete 문 처리](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)  
  
-   [SELECT FOR UPDATE 문 처리](../../../odbc/reference/appendixes/processing-select-for-update-statements.md)  
  
-   [SQL 문의 일괄 처리](../../../odbc/reference/appendixes/processing-batches-of-sql-statements.md)  
  
-   [검색된 문 생성](../../../odbc/reference/appendixes/constructing-searched-statements.md)
