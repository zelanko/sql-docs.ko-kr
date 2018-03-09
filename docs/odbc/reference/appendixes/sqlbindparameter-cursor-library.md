---
title: "SQLBindParameter (커서 라이브러리) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLBindParameter function [ODBC], Cursor Library
ms.assetid: 04c53e4c-cd1d-40b2-9997-684ebe43499f
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a6fb1b8e369b70d8bb5a1fa38ebc9dd6ea2906ed
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter (커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목의 사용을 설명는 **SQLBindParameter** 커서 라이브러리의 함수가 있습니다. 에 대 한 일반적인 내용은 **SQLBindParameter**, 참조 [SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)합니다.  
  
 응용 프로그램에서 호출할 수 **SQLBindParameter** C 데이터 형식, 열 크기 및 연결된 된 필드의 10 진수 동일 하 게 유지으로 매개 변수를 다시 바인딩해야 합니다.  
  
 커서 라이브러리 지원 SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성 바인딩 오프셋을 사용 하도록 설정 합니다. (**SQLBindParameter** 되려면 리바인딩이 대해 호출할 필요는 없습니다.)  
  
 커서 라이브러리 바인딩 실행 시 데이터 매개 변수를 지원 합니다.
