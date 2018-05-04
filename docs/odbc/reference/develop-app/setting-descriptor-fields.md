---
title: 설명자 필드 설정 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: d735dc64-370f-48ab-a59f-6cef9bc4e1e8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5ea00d83f1f57498ee1094264c1895f50103526c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="setting-descriptor-fields"></a>설명자 필드 설정
응용 프로그램이 호출할 수는 설명자 필드를 수정 하려면 **SQLSetDescField**합니다. 일부 필드는 읽기 전용 이며 설정할 수 없습니다. (참조는 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 함수 설명 합니다.)  
  
 레코드 번호 설명자 레코드 필드 설정 됩니다 (*RecNumber*) 1 이상이 while 설명자 헤더 필드는 레코드 번호 0으로 설정 됩니다. 책갈피 0 열에 포함 된 규칙에 따라 책갈피 필드를 설정 하는 레코드 번호 0도 사용 됩니다. 이 책갈피 필드 설명자 헤더 내에 포함 되어 있지만이 대/소문자 인상을 상태로 될 수 있습니다. 책갈피 필드가 헤더 필드에서 고유 합니다.  
  
 응용 프로그램에 정의 된 순서를 따라야 필드를 개별적으로 설정할 때 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)합니다. 일부 필드를 설정 하면 드라이버를 다른 필드를 설정 합니다. 이렇게 하면 설명자는 언제 든 지는 응용 프로그램에서 데이터 형식이 지정 되 면 사용 하도록 합니다. SQL_DESC_TYPE 필드를 설정 하는 응용 프로그램, 드라이버 유형을 지정 하는 다른 필드는 유효 하 고 일관 된 있는지 확인 합니다.  
  
 설명자 필드를 설정 하는 함수 호출에 실패 하면 설명자 필드의 내용을 정의 되지 않습니다 실패 한 함수 호출 후.
