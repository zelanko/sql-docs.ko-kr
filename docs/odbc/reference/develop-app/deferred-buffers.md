---
description: 지연 버퍼
title: 지연 된 버퍼 | Microsoft Docs
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
ms.openlocfilehash: 320271c39c735eafcfb1d59d26e7d0400eaa6e6c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424705"
---
# <a name="deferred-buffers"></a>지연 버퍼
*지연 된 버퍼* 는 함수 호출에서 값이 지정 된 *후* 에 해당 값이 사용 되는 버퍼입니다. 예를 들어 **SQLBindParameter** 를 사용 하 여 데이터 버퍼를 SQL 문의 매개 변수와 연결 하거나 *바인딩합니다* . 응용 프로그램은 매개 변수 번호를 지정 하 고 주소, 바이트 길이 및 버퍼 형식을 전달 합니다. 드라이버는이 정보를 저장 하지만 버퍼의 내용을 검사 하지 않습니다. 나중에 응용 프로그램에서 문을 실행할 때 드라이버는 정보를 검색 하 고이를 사용 하 여 매개 변수 데이터를 검색 하 고 데이터 원본으로 보냅니다. 따라서 버퍼의 데이터 입력이 지연 됩니다. 지연 된 버퍼는 한 함수에서 지정 되 고 다른 함수에서 사용 되므로 드라이버가 여전히 존재 하는 동안 지연 된 버퍼를 해제 하는 것은 응용 프로그램 프로그래밍 오류입니다. 자세한 내용은이 섹션의 뒷부분에 나오는 [버퍼 할당 및 해제](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)를 참조 하세요.  
  
 입력 및 출력 버퍼는 모두 지연 될 수 있습니다. 다음 표에는 지연 된 버퍼의 사용이 요약 되어 있습니다. 결과 집합 열에 바인딩된 지연 된 버퍼는 **SQLBindCol**를 사용 하 여 지정 되 고 SQL 문 매개 변수에 바인딩된 지연 버퍼는 **SQLBindParameter**로 지정 됩니다.  
  
|버퍼 사용|Type|지정 된|사용 대상|  
|----------------|----------|--------------------|-------------|  
|입력 매개 변수에 대 한 데이터 보내기|지연 된 입력|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|결과 집합에서 행을 업데이트 하거나 삽입 하기 위해 데이터 보내기|지연 된 입력|**SQLBindCol**|**SQLSetPos**|  
|출력 및 입/출력 매개 변수에 대 한 데이터 반환|지연 된 출력|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|결과 집합 데이터 반환|지연 된 출력|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|
