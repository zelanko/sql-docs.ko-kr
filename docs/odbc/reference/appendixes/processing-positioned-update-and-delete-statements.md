---
description: 위치 지정 업데이트 및 Delete 문 처리
title: 위치 지정 업데이트 및 Delete 문 처리 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- ODBC cursor library [ODBC], statement processing
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- SQL statements [ODBC], cursor library
- ODBC cursor library [ODBC], positioned update or delete
- cursor library [ODBC], statement processing
ms.assetid: 2975dd97-48e6-4d0a-a9c7-40759a7d94c8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f11e5acd8afe46397126ddb4c1d4127eb99fc67a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483206"
---
# <a name="processing-positioned-update-and-delete-statements"></a>위치 지정 업데이트 및 Delete 문 처리
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 커서 라이브러리는 이러한 문에서 **WHERE CURRENT OF** 절을 where 절로 바꾸고 각 바인딩된 열에 대해 해당 캐시에 저장 된 값을 열거 하는 방법 **으로 위치 지정** update 및 delete 문을 지원 합니다. 커서 라이브러리는 새로 생성 된 **UPDATE** 및 **DELETE** 문을 실행을 위해 드라이버에 전달 합니다. 위치 지정 update 문의 경우 커서 라이브러리는 행 집합 버퍼의 값에서 캐시를 업데이트 하 고 행 상태 배열의 해당 값을 SQL_ROW_UPDATED로 설정 합니다. 배치 된 delete 문의 경우 행 상태 배열의 해당 값을 SQL_ROW_DELETED로 설정 합니다.  
  
> [!CAUTION]  
>  현재 행을 식별 하기 위해 커서 라이브러리로 생성 된 **where** 절은 행을 식별 하거나 다른 행을 식별 하거나 둘 이상의 행을 식별 하는 데 실패할 수 있습니다. 자세한 내용은이 부록의 뒷부분에 나오는 [검색 문 생성](../../../odbc/reference/appendixes/constructing-searched-statements.md)을 참조 하세요.  
  
 위치 지정 update 및 delete 문에는 다음과 같은 제한 사항이 적용 됩니다.  
  
-   위치 지정 업데이트 및 delete 문은 **SELECT** 문에서 결과 집합을 생성 하는 경우에만 사용할 수 있습니다. **SELECT** 문에 Join, **UNION** 절 또는 **group BY** 절이 포함 되지 않은 경우 select 목록에서 별칭이 나 식을 사용한 열이 **SQLBindCol**과 바인딩되지 않은 경우  
  
-   응용 프로그램에서 위치 지정 update 또는 delete 문을 준비 하는 경우 **Sqlfetch** 또는 **sqlfetchscroll**을 호출한 후에 수행 해야 합니다. 커서 라이브러리는 준비를 위해 문을 드라이버에 제출 하지만 응용 프로그램이 **Sqlexecute**를 호출 하면 문을 닫고 직접 실행 합니다.  
  
-   드라이버가 하나의 활성 문만 지 원하는 경우 커서 라이브러리는 그 나머지 결과 집합을 인출 하 고 현재 행 집합을 캐시에서 refetches 위치 지정 update 또는 delete 문을 실행 합니다. 그러면 응용 프로그램에서 결과 집합의 메타 데이터를 반환 하는 함수를 호출 하는 경우 (예: **Sqlnumresultcols** 또는 **SQLDescribeCol**) 커서 라이브러리에서 오류를 반환 합니다.  
  
-   업데이트를 수행할 때마다 자동으로 업데이트 되는 타임 스탬프 열이 포함 된 테이블의 열에 대해 위치 지정 update 또는 delete 문을 수행 하는 경우 타임 스탬프 열이 바인딩되면 이후의 모든 update 또는 delete 문이 실패 합니다. 이는 커서 라이브러리가 만드는 검색 된 update 또는 delete 문이 업데이트할 행을 정확 하 게 식별 하지 못하기 때문에 발생 합니다. Timestamp 열에 대 한 검색 된 문의 값이 자동으로 업데이트 된 timestamp 열의 값과 일치 하지 않습니다.
