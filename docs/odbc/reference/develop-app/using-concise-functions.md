---
description: 간결한 함수 사용
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b0dcd16c1380c95921d5e4bb58831e2dd939ecf1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482799"
---
# <a name="using-concise-functions"></a>간결한 함수 사용
일부 ODBC 함수는 설명자에 대 한 암시적 액세스 권한을 얻습니다. 응용 프로그램 작성자가 **SQLSetDescField** 또는 **SQLGetDescField**를 호출 하는 것 보다 더 편리할 수 있습니다. 이러한 함수는 설명자 필드 설정 또는 가져오기를 포함 하 여 다양 한 함수를 수행 하기 때문에 *간결한* 함수 라고 합니다. 일부 간결한 함수를 사용 하면 응용 프로그램이 단일 함수 호출에서 여러 관련 설명자 필드를 설정 하거나 검색할 수 있습니다.  
  
 간결한 함수는 인수로 사용할 설명자 핸들을 먼저 검색 하지 않고 호출할 수 있습니다. 이러한 함수는 호출 되는 문 핸들과 연결 된 설명자 필드에서 작동 합니다.  
  
 간결한 함수 **SQLBindCol** 및 **SQLBindParameter** 는 해당 인수에 해당 하는 설명자 필드를 설정 하 여 열 또는 매개 변수를 바인딩합니다. 이러한 각 함수는 단순히 설명자를 설정 하는 것 보다 더 많은 작업을 수행 합니다. **SQLBindCol** 및 **SQLBindParameter** 는 데이터 열 또는 동적 매개 변수의 바인딩을 완벽 하 게 지정 합니다. 그러나 응용 프로그램은 **SQLSetDescField** 또는 **SQLSetDescRec** 를 호출 하 여 바인딩의 개별 정보를 변경 하 고 이러한 함수에 대 한 일련의 적절 한 호출을 수행 하 여 열 또는 매개 변수를 완전히 바인딩할 수 있습니다.  
  
 간결한 함수 **Sqlcolattribute**, **SQLDescribeCol**, **SQLDescribeParam**, **Sqlcolattribute**및 **sqlnumresultcols** 는 설명자 필드의 값을 검색 합니다.  
  
 **SQLSetDescRec** 및 **SQLGetDescRec** 은 한 번의 호출로, 열 또는 매개 변수 데이터의 데이터 형식 및 저장소에 영향을 주는 여러 설명자 필드를 설정 하거나 가져오는 간결한 함수입니다. **SQLSetDescRec** 는 한 번에 열 또는 매개 변수 데이터의 바인딩을 변경 하는 효과적인 방법입니다.  
  
 **SQLSetStmtAttr** 및 **SQLGetStmtAttr** 는 경우에 따라 간결한 함수 역할을 합니다. [설명자 필드](../../../odbc/reference/develop-app/descriptor-fields.md)를 참조 하세요.
