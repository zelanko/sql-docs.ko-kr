---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7943987d52554e0f5cd7723e8c9ae8a0e3afddd2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093034"
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는의 사용을 설명 합니다 **SQLBindParameter** 커서 라이브러리의 함수입니다. 에 대 한 일반 정보에 대 한 **SQLBindParameter**를 참조 하십시오 [SQLBindParameter 함수](../../../odbc/reference/syntax/sqlbindparameter-function.md)합니다.  
  
 응용 프로그램에서 호출할 수 있습니다 **SQLBindParameter** C 데이터 형식, 열 크기 및 연결된 된 필드의 10 진수 남아 동일한 매개 변수를 다시 바인딩해야 합니다.  
  
 커서 라이브러리 지원 SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성 바인딩 오프셋을 사용 하도록 설정 합니다. (**SQLBindParameter** 이렇게 다시 바인딩하기 위해서는 발생에 대해 호출할 필요가 없습니다.)  
  
 커서 라이브러리 바인딩 실행 시 데이터 매개 변수를 지원합니다.
