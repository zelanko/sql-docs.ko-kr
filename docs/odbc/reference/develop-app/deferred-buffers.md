---
title: 이연 버퍼 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- buffers [ODBC], deferred
- deferred buffers [ODBC]
ms.assetid: 02c9a75c-2103-4f68-a1db-e31f7e0f1f03
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f34c6d3d886a0a75c309dc4f5c71f5c7ba3df447
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305984"
---
# <a name="deferred-buffers"></a>지연 버퍼
*지연된 버퍼는* 함수 호출에 지정된 *후* 어느 시점에 값이 사용되는 버퍼입니다. 예를 들어 **SQLBindParameter는** SQL 문의 매개 변수와 데이터 버퍼를 연결하거나 *바인딩하는* 데 사용됩니다. 응용 프로그램은 매개 변수의 수를 지정하고 주소, 바이트 길이 및 버퍼의 형식을 전달합니다. 드라이버는 이 정보를 저장하지만 버퍼의 내용을 검사하지 는 않습니다. 나중에 응용 프로그램이 문을 실행하면 드라이버는 정보를 검색하고 이를 사용하여 매개 변수 데이터를 검색하고 데이터 원본으로 보냅니다. 따라서 버퍼에 있는 데이터의 입력이 지연됩니다. 지연 된 버퍼는 한 함수에 지정 되고 다른 함수에서 사용 되기 때문에 드라이버가 여전히 존재 할 것으로 예상 하는 동안 지연 된 버퍼를 해제 하는 응용 프로그램 프로그래밍 오류입니다. 자세한 내용은 이 섹션의 후반부에서 [버퍼 할당 및 해제를](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)참조하십시오.  
  
 입력 버퍼와 출력 버퍼를 모두 연기할 수 있습니다. 다음 표에서는 지연된 버퍼의 사용을 요약합니다. 결과 집합 열에 바인딩된 연기된 버퍼는 **SQLBindCol으로**지정되며 SQL 문 매개 변수에 바인딩된 지연 버퍼는 **SQLBindParameter**.  
  
|버퍼 사용|Type|를 지정합니다.|사용 대상|  
|----------------|----------|--------------------|-------------|  
|입력 매개 변수에 대한 데이터 전송|지연된 입력|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|결과 집합에서 행을 업데이트하거나 삽입하기 위해 데이터 보내기|지연된 입력|**SQLBindCol**|**SQLSetPos**|  
|출력 및 입력/출력 매개 변수에 대한 데이터 반환|지연된 출력|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|결과 집합 데이터 반환|지연된 출력|**SQLBindCol**|**SQLFetch**<br /> **SQLFetch스크롤 SQLSetPos**|
