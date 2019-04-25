---
title: 설명자 필드 초기화 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- initializing descriptor fields [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1da157cb-8ea9-4a56-983b-1c45650217c5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d988099cad357254f04a79a8a6cccbbe4eb2768c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62446814"
---
# <a name="initialization-of-descriptor-fields"></a>설명자 필드 초기화
응용 프로그램 행 설명자를 할당 하는 경우 해당 필드에 표시 된 대로 초기 값을 수신 하는 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)합니다. SQL_DESC_TYPE 필드의 초기 값은 SQL_DEFAULT 합니다. 이 프레젠테이션 응용 프로그램에 대 한 데이터베이스 데이터의 표준 처리를 제공합니다. 응용 프로그램 설명자 레코드의 필드를 설정 하 여 데이터의 다른 처리를 지정할 수 있습니다.  
  
 설명자 헤더의 SQL_DESC_ARRAY_SIZE의 초기 값은 1입니다. 응용 프로그램 다중 행 페치를 사용 하도록 설정 하려면이 필드를 수정할 수 있습니다.  
  
 기본값의 개념 IRD 필드에 대해 올바르지 않습니다. 응용 프로그램 실행 또는 준비 된 문을 연결 된 경우에 IRD 필드에 대 한 액세스를 얻을 수 있습니다.  
  
 특정 필드는 IPD의 IPD가 드라이버에서 자동으로 입력 된 후에 정의 됩니다. 그렇지 않은 경우 정의 되지 않습니다. 이러한 필드는 SQL_DESC_CASE_SENSITIVE "," SQL_DESC_FIXED_PREC_SCALE "," 인 SQL_DESC_TYPE_NAME "," SQL_DESC_UNSIGNED, "및" SQL_DESC_LOCAL_TYPE_NAME 합니다.
