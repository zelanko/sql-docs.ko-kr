---
title: 지연 버퍼 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b071494697d21a37f4420889a8f60cc35fe3d8b2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63049889"
---
# <a name="deferred-buffers"></a>지연 버퍼
A *지연 된 버퍼* 값인 언젠가 하나인 *후* 함수 호출에 지정 된 합니다. 예를 들어 **SQLBindParameter** 에 연결 하는 데 사용 됩니다 또는 *바인딩* SQL 문에서 매개 변수를 사용 하 여 데이터 버퍼입니다. 응용 프로그램 매개 변수 개수를 지정 하 고 주소, 바이트 길이 및 버퍼 유형의 전달 합니다. 드라이버는이 정보를 저장 했지만 버퍼의 내용을 검사 하지 않습니다. 나중에 문을 실행 하는 응용 프로그램, 드라이버 정보를 검색 한 데이터 원본에 보내는 매개 변수 데이터를 검색 하는 데 사용 합니다. 따라서 버퍼의 데이터 입력 지연 됩니다. 지연 된 버퍼는 하나의 함수에 지정 되 고 다른 사용, 이므로 응용 프로그램 프로그래밍 오류 드라이버 여전히 존재 하는 동안 지연 된 버퍼를 해제 하려면 자세한 내용은 [Allocating 및 버퍼 해제](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)이 섹션의 뒷부분에 나오는.  
  
 입력 및 출력 버퍼를 지연 시킬 수 있습니다. 다음 표에서 지연 된 버퍼의 사용을 보여 줍니다. 결과 집합 열에 바인딩된 지연 된 버퍼가 사용 하 여 지정 됩니다 **SQLBindCol**를 사용 하 여 SQL 문의 매개 변수에 바인딩된 지연 된 버퍼는 지정 **SQLBindParameter**합니다.  
  
|버퍼 사용|형식|지정 된|사용 대상|  
|----------------|----------|--------------------|-------------|  
|입력된 매개 변수에 대 한 데이터 전송|지연 된 입력|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|데이터를 결과에서 행을 삽입 하거나 업데이트할 전송 설정|지연 된 입력|**SQLBindCol**|**SQLSetPos**|  
|출력 및 입/출력 매개 변수는 데이터를 반환합니다.|지연 된 출력|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|데이터 집합 결과 반환 합니다.|지연 된 출력|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|
