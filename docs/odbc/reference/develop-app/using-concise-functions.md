---
title: 간결한 함수 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- concise functions [ODBC]
- functions [ODBC], concise functions
- descriptors [ODBC], concise functions
ms.assetid: 31ac070f-8c59-4fd5-bd5a-466bb27dbca0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d70d3ca60a046a355549260406edba261f805e4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63312477"
---
# <a name="using-concise-functions"></a>간결한 함수 사용
일부 ODBC 함수에는 암시적 설명자 액세스할을 수 있습니다. 응용 프로그램 작성자 더 편리할 수 고 호출 보다 **SQLSetDescField** 하거나 **SQLGetDescField**합니다. 이러한 함수가 호출 될 *간결한* 여러 기능을 설정 하거나 가져오기 설명자 필드를 포함 하 여 수행 하기 때문에 작동 합니다. 일부 간결한 함수를 사용 하는 응용 프로그램 설정 또는 단일 함수 호출의 몇 가지 관련된 설명자 필드를 검색 합니다.  
  
 간결한 함수는 첫 번째 인수로 사용에 대 한 설명자 핸들을 검색 하지 않고 호출할 수 있습니다. 이러한 함수에서 호출 되는 문 핸들을 사용 하 여 연결 된 설명자 필드를 사용 하 여 작동 합니다.  
  
 간결한 함수 **SQLBindCol** 하 고 **SQLBindParameter** 해당 인수에 해당 하는 설명자 필드를 설정 하 여 열 또는 매개 변수를 바인딩합니다. 이러한 각 함수는 단순히 설명자를 설정 하는 보다 자세한 작업을 수행 합니다. **SQLBindCol** 하 고 **SQLBindParameter** 데이터 열 이나 동적 매개 변수 바인딩의 완전 한 사양을 제공 합니다. 그러나 호출 하 여 응용 프로그램 바인딩의 개인 정보를 변경할 수 있습니다 **SQLSetDescField** 하거나 **SQLSetDescRec** 일련의 적합 한 호출 하 여 열 또는 매개 변수를 바인딩할 완전히 수 및 이러한 함수입니다.  
  
 간결한 함수 **SQLColAttribute**, **SQLDescribeCol**, **SQLDescribeParam**하십시오 **SQLNumParams**, 및  **SQLNumResultCols** 설명자 필드 값을 검색 합니다.  
  
 **SQLSetDescRec** 하 고 **SQLGetDescRec** 간결한 함수를 한 번의 호출을 사용 하 여 데이터 형식 및 열 또는 매개 변수 데이터의 저장소에 영향을 주는 여러 설명자 필드를 가져오거나 설정 합니다. **SQLSetDescRec** 은 한 번에 열 또는 매개 변수 데이터의 바인딩을 변경 하는 효과적인 방법입니다.  
  
 **SQLSetStmtAttr** 하 고 **SQLGetStmtAttr** 경우도 간결한 함수 역할도 합니다. (참조 [설명자 필드](../../../odbc/reference/develop-app/descriptor-fields.md).)
