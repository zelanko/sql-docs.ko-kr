---
description: SQLBindParameter(커서 라이브러리)
title: SQLBindParameter (커서 라이브러리) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindParameter function [ODBC], Cursor Library
ms.assetid: 04c53e4c-cd1d-40b2-9997-684ebe43499f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96fb4f3390b062a4b86f7a7b7f457c43c476c26c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466075"
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLBindParameter** 함수를 사용 하는 방법을 설명 합니다. **SQLBindParameter**에 대 한 일반 정보는 [SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)를 참조 하세요.  
  
 바인딩된 열의 C 데이터 형식, 열 크기 및 10 진수가 동일 하 게 유지 되는 한 응용 프로그램은 **SQLBindParameter** 를 호출 하 여 매개 변수를 다시 바인딩할 수 있습니다.  
  
 커서 라이브러리는 바인딩 오프셋을 사용 하도록 SQL_ATTR_ROW_BIND_OFFSET_PTR statement 특성을 설정 하도록 지원 합니다. 이 리바인딩을 수행 하기 위해**SQLBindParameter** 를 호출할 필요가 없습니다.  
  
 커서 라이브러리는 실행 시 데이터 바인딩 매개 변수를 지원 합니다.
