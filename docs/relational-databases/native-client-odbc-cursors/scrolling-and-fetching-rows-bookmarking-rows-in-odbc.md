---
title: ODBC의 행 책갈피 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], fetching rows
- ODBC cursors, fetching rows
- cursors [ODBC], scrolling rows
- ODBC cursors, scrolling rows
- bookmarks [ODBC]
ms.assetid: 9cfcd243-c9d4-4c2a-abc4-399dbabe5f6b
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fc90fd2a24e8850922e45d17fb331ce412dde482
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73784089"
---
# <a name="scrolling-and-fetching-rows---bookmarking-rows-in-odbc"></a>행 스크롤 및 페치 - ODBC에서 행에 책갈피 지정
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  책갈피는 데이터의 행을 식별하는 데 사용되는 값입니다. 책갈피 값의 의미는 드라이버나 데이터 원본에만 알려집니다. 예를 들어 책갈피 값은 행 번호처럼 간단하거나 디스크 주소처럼 복잡할 수 있습니다. ODBC 애플리케이션에서는 특정 행에 대해 책갈피를 요청하고 이를 저장한 다음 다시 커서에 전달하여 원래 행으로 돌아갑니다.  
  
 [Sqlfetchscroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)을 사용 하 여 행을 인출 하는 경우 응용 프로그램은 시작 행을 선택 하기 위한 기준으로 책갈피를 사용할 수 있습니다. 이 책갈피는 현재 커서 위치를 사용하지 않기 때문에 절대 주소 형태로 되어 있습니다. 책갈피가 설정 된 행으로 스크롤하려면 응용 프로그램은 SQL_FETCH_BOOKMARK의 *Fetchorientation* 로 **sqlfetchscroll** 을 호출 합니다. 이 작업은 SQL_ATTR_FETCH_BOOKMARK_PTR 옵션 특성이 가리키는 책갈피를 사용하며 이 책갈피를 통해 식별된 행부터 행 집합을 반환합니다. 응용 프로그램은 **Sqlfetchscroll**에 대 한 호출의 *fetchoffset* 인수에서이 작업에 대 한 오프셋을 지정할 수 있습니다. 오프셋이 지정되면 책갈피를 통해 식별된 행 수에 FetchOffset 인수에 지정된 숫자를 더하는 방식으로 반환된 행 집합의 첫 번째 행이 결정됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 정적 및 키 집합 커서에 대해서만 책갈피를 지원합니다. 책갈피가 설정되어 있을 때 동적 커서가 요청되면 키 집합 커서가 대신 열립니다.  
  
 책갈피를 **SQLBulkOperations** 함수와 함께 사용 하 여 책갈피에서 시작 하는 행 집합에 대 한 작업을 수행할 수도 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [행 스크롤 및 페치](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows.md)  
  
  
