---
title: SQLRowCount (커서 라이브러리) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLRowCount function [ODBC], Cursor Library
ms.assetid: 781cf5a5-325e-4523-8633-d96d9e98277c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf9fe597f54ecb4bc82439251e2228ac5fdc4ea3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300593"
---
# <a name="sqlrowcount-cursor-library"></a>SQLRowCount(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLRowCount** 함수의 사용에 대해 설명합니다. **SQLRowCount에**대한 일반 정보는 [SQLRowCount 함수를](../../../odbc/reference/syntax/sqlrowcount-function.md)참조하십시오.  
  
 응용 프로그램이 **SQLRowCount를** 커서와 연결된 문으로 호출하면 커서 라이브러리는 드라이버에서 검색한 데이터 행 수를 반환합니다.  
  
 응용 프로그램이 **SQLRowCount를** 위치 업데이트 또는 delete 문과 연결된 문으로 호출하면 커서 라이브러리는 명령문에 영향을 받는 행 수를 반환합니다.  
  
 응용 프로그램이 **SELECT** 문 다음에 **SQLRowCount를** 호출하면 커서 라이브러리가 -1을 반환합니다.
