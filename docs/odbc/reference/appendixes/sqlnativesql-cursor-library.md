---
title: SQLNativeSql (커서 라이브러리) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLNativeSql function [ODBC], Cursor Library
ms.assetid: c4459092-1177-4b2a-b7f5-e0083d3bf2b2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 41f7617530f34d49852ca67db9f47cab94292385
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300573"
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLNativeSql** 함수의 사용에 대해 설명합니다. **SQLNativeSql에**대한 일반적인 내용은 [SQLNativeSql 함수를](../../../odbc/reference/syntax/sqlnativesql-function.md)참조하십시오.  
  
 드라이버가 이 함수를 지원하는 경우 커서 라이브러리는 드라이버에서 **SQLNativeSql을** 호출하고 SQL 문을 전달합니다. 위치 업데이트, 위치 삭제 및 **UPDATE용 SELECT** 문의 경우 커서 라이브러리는 명령문을 드라이버에 전달하기 전에 수정합니다.  
  
> [!NOTE]  
>  커서 라이브러리잘못 반환 SQLSTATE 34000 (잘못된 커서 이름) 커서 이름이 위치 된 업데이트또는 **SQLNativeSql의** *InStatementText* 인수에 전달 되는 문을 삭제 잘못 된 경우 **SQLNativeSql은** 문 준비 또는 실행 시에만 반환되는 구문 오류를 반환하기 위한 것이 아닙니다.
