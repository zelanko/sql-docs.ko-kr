---
title: 간결한 기능 사용 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 63313e3dfaec8dbcd91f3bb084bbaab46da40c6e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306784"
---
# <a name="using-concise-functions"></a>간결한 함수 사용
일부 ODBC 함수는 설명자에 대한 암시적 액세스 권한을 얻습니다. 응용 프로그램 작성기는 **SQLSetDescField 또는 SQLGetDescField를** 호출하는 것보다 더 편리 할 수 있습니다. **SQLGetDescField** 이러한 함수는 설명자 필드 설정 또는 가져오는 등 여러 함수를 수행하기 때문에 *간결한* 함수라고 합니다. 일부 간결한 함수를 사용하면 응용 프로그램이 단일 함수 호출에서 여러 관련 설명자 필드를 설정하거나 검색할 수 있습니다.  
  
 간결한 함수는 먼저 인수로 사용하기 위해 설명자 핸들을 검색하지 않고 호출할 수 있습니다. 이러한 함수는 호출되는 문 핸들과 연결된 설명자 필드와 함께 작동합니다.  
  
 간결한 함수 **SQLBindCol** 및 **SQLBindParameter** 해당 인수에 해당 하는 설명자 필드를 설정 하 여 열 또는 매개 변수를 바인딩합니다. 이러한 각 함수는 단순히 설명자 설정보다 더 많은 작업을 수행합니다. **SQLBindCol** 및 **SQLBindParameter** 는 데이터 열 또는 동적 매개 변수의 바인딩에 대한 전체 사양을 제공합니다. 그러나 응용 프로그램은 **SQLSetDescField** 또는 **SQLSetDescRec를** 호출하여 바인딩의 개별 세부 정보를 변경할 수 있으며 이러한 함수에 대한 일련의 적절한 호출을 만들어 열이나 매개 변수를 완전히 바인딩할 수 있습니다.  
  
 간결한 함수 **SQLColAttribute,** **SQLDescribeCol,** **SQLDescribeParam,** **SQLNumParams**및 **SQLNumResultCols는** 설명자 필드에서 값을 검색합니다.  
  
 **SQLSetDescRec** 및 **SQLGetDescRec는** 하나의 호출로 열 또는 매개 변수 데이터의 데이터 형식 및 저장소에 영향을 주는 여러 설명자 필드를 설정하거나 받는 간결한 함수입니다. **SQLSetDescRec는** 한 단계에서 열 또는 매개 변수 데이터의 바인딩을 변경하는 효과적인 방법입니다.  
  
 **SQLSetStmtAttr** 및 **SQLGetStmtAttr은** 경우에 따라 간결한 함수역할을 합니다. [(설명자 필드](../../../odbc/reference/develop-app/descriptor-fields.md)참조))
