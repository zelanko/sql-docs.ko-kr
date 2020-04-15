---
title: SQL 문 처리 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eda640f6e810eeccbfa17ea2b6ba7c1b19b28e08
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81308004"
---
# <a name="processing-sql-statements"></a>SQL 문 처리
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 ODBC 커서 라이브러리는 다음을 제외한 모든 SQL 문을 드라이버에 직접 전달합니다.  
  
-   위치 업데이트 및 삭제 문  
  
-   업데이트 문을 **선택합니다.**  
  
-   일괄 처리된 SQL 문  
  
 위치 가있는 업데이트를 실행하고 문을 삭제하고 해당 행에 대해 **SQLGetData를** 호출하기 위해 행에 커서를 배치하려면 커서 라이브러리는 행을 식별하는 검색된 문을 생성합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [위치 지정 업데이트 및 Delete 문 처리](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)  
  
-   [SELECT FOR UPDATE 문 처리](../../../odbc/reference/appendixes/processing-select-for-update-statements.md)  
  
-   [SQL 문의 일괄 처리](../../../odbc/reference/appendixes/processing-batches-of-sql-statements.md)  
  
-   [검색된 문 생성](../../../odbc/reference/appendixes/constructing-searched-statements.md)
