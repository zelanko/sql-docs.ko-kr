---
title: SQLBind매개 변수 (커서 라이브러리) | 마이크로 소프트 문서
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
ms.openlocfilehash: 55708cc5192fb40149d6db7710f6ee638c4880d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305431"
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLBindParameter** 함수의 사용에 대해 설명합니다. **SQLBind매개 변수에**대한 일반 정보는 [SQLBind매개 변수 함수를](../../../odbc/reference/syntax/sqlbindparameter-function.md)참조하십시오.  
  
 응용 프로그램은 바인딩된 열의 C 데이터 형식, 열 크기 및 소수 자릿수가 동일하게 유지되는 한 **SQLBindParameter를** 호출하여 매개 변수를 다시 바인딩할 수 있습니다.  
  
 커서 라이브러리는 바인드 오프셋을 사용하도록 SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성 설정에 지원됩니다. (이 재바인딩이 발생하기 위해**SQLBindParameter를** 호출할 필요는 없습니다.)  
  
 커서 라이브러리는 실행 시 데이터 바인딩 매개 변수를 지원합니다.
