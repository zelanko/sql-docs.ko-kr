---
title: "간결 하 게 함수를 사용 하 여 | Microsoft Docs"
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
- concise functions [ODBC]
- functions [ODBC], concise functions
- descriptors [ODBC], concise functions
ms.assetid: 31ac070f-8c59-4fd5-bd5a-466bb27dbca0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5559250002983b942601311b04e1f4ae2eac49a2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="using-concise-functions"></a>간결 하 게 함수를 사용 하 여
일부 ODBC 함수 설명자를 암시적으로 액세스할을 수 있습니다. 응용 프로그램 작성자 사실을 알 수 있을 호출 보다 편리 하 게 **SQLSetDescField** 또는 **SQLGetDescField**합니다. 이 함수가 호출 될 *간결한* 다양 한을 설정 하거나 가져오기 설명자 필드를 비롯 한 함수를 수행 하기 때문에 작동 합니다. 일부 간결 하 게 함수를 사용 하는 응용 프로그램을 설정 하거나 단일 함수 호출에서 여러 관련된 설명자 필드를 검색 합니다.  
  
 첫 번째 인수로 사용에 대 한 설명자 핸들을 검색 하지 않고 간결 하 게 함수를 호출할 수 있습니다. 이러한 함수에 호출 될 때 문 핸들에 연결 된 설명자 필드를 사용 합니다.  
  
 간결한 함수 **SQLBindCol** 및 **SQLBindParameter** 해당 인수에 해당 하는 설명자 필드를 설정 하 여 열 또는 매개 변수를 바인딩합니다. 이러한 각 함수는 설명자를 설정 하면 보다 많은 작업을 수행 합니다. **SQLBindCol** 및 **SQLBindParameter** 데이터 열 또는 동적 매개 변수 바인딩이의 완전 한 사양을 제공 합니다. 그러나 응용 프로그램 호출 하 여 바인딩 개인 정보를 변경할 수 **SQLSetDescField** 또는 **SQLSetDescRec** 일련의 적합 한 호출을 하 여 열 또는 매개 변수를 바인딩할 완전히 수 있습니다 이러한 함수입니다.  
  
 간결한 함수 **SQLColAttribute**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLNumParams**, 및 ** SQLNumResultCols** 설명자 필드에서 값을 검색 합니다.  
  
 **SQLSetDescRec** 및 **SQLGetDescRec** 는 간결 하 게 하는 함수를 한 번의 호출으로 데이터 형식 및 열 또는 매개 변수 데이터의 저장소에 영향을 주는 여러 설명자 필드를 가져오거나 설정 합니다. **SQLSetDescRec** 은 한 번에 열 또는 매개 변수 데이터의 바인딩을 변경 하는 효과적인 방법입니다.  
  
 **SQLSetStmtAttr** 및 **SQLGetStmtAttr** 역할 경우에 따라 간결 하 게 기능을 수행 합니다. (참조 [설명자 필드](../../../odbc/reference/develop-app/descriptor-fields.md).)
