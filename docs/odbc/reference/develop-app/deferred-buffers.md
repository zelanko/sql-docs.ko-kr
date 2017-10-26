---
title: "버퍼를 지연 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- buffers [ODBC], deferred
- deferred buffers [ODBC]
ms.assetid: 02c9a75c-2103-4f68-a1db-e31f7e0f1f03
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 94d240284ce0273e0700bfbabfb38fd0a41884cf
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="deferred-buffers"></a>지연 된 버퍼
A *지연 된 버퍼* 시간에는 값이 사용 되는 *후* 함수 호출에 지정 되어 있습니다. 예를 들어 **SQLBindParameter** 를 연결 하는 데 사용 됩니다 또는 *바인딩* SQL 문에서 매개 변수를 사용 하 여 데이터 버퍼입니다. 응용 프로그램 매개 변수 수를 지정 하 고는 주소, 바이트 길이 및 버퍼의 종류를 전달 합니다. 드라이버는이 정보는 저장 되지만 버퍼의 내용을 검사 하지 않습니다. 이상에서는 문을 실행 하는 응용 프로그램, 드라이버 정보를 검색 한 하는 매개 변수 데이터를 검색 하 고 데이터 원본에 보내는 데 사용 합니다. 따라서 버퍼에 데이터의 입력 지연 됩니다. 지연 된 버퍼 하나의 함수에 지정 된 다른 사용 되는, 되므로 응용 프로그램 프로그래밍 오류를 드라이버 여전히 기대에 존재 하는 동안 지연 된 버퍼를 해제 자세한 내용은 참조 [Allocating 및 버퍼 해제](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)이 섹션의 뒷부분에 나오는 합니다.  
  
 입력 및 출력 버퍼를 지연 시킬 수 있습니다. 다음 표에서 지연 된 버퍼의 사용을 요약 합니다. 지연 된 버퍼에 결과 집합 열의 바인딩된와 지정 된 **SQLBindCol**, 지연 된 SQL 문의 매개 변수에 바인딩되어 버퍼와 및 **SQLBindParameter**합니다.  
  
|버퍼 사용|형식|지정 된|사용 대상|  
|----------------|----------|--------------------|-------------|  
|입력된 매개 변수에 대 한 데이터 보내기|지연 된 입력|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|결과에서 행을 삽입 하거나 업데이트할를 보내는 데이터 집합|지연 된 입력|**SQLBindCol**|**SQLSetPos**|  
|출력 및 입/출력 매개 변수는 데이터 반환|지연 된 출력|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|데이터 집합 결과 반환 합니다.|지연 된 출력|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|

