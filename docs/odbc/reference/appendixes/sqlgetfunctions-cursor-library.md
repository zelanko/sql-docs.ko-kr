---
title: SQLGetFunctions (커서 라이브러리) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetFunctions function [ODBC], Cursor Library
ms.assetid: 931acd12-4eb6-4a78-9a77-157a18a9a2d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f993a08aae1656b8d373911299e75852de855419
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307824"
---
# <a name="sqlgetfunctions-cursor-library"></a>SQLGetFunctions(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLGetFunctions** 함수의 사용에 대해 설명합니다. **SQLGetFunctions에**대한 일반적인 내용은 [SQLGetFunctions 함수를](../../../odbc/reference/syntax/sqlgetfunctions-function.md)참조하십시오.  
  
 **SQLGetFunctions를**호출하면 커서 라이브러리는 드라이버에서 지원하는 함수 외에 **SQLExtendedFetch,** **SQLFetch스크롤,** **SQLSetPos**및 **SQLSetScrollOptions를**지원하는 것을 반환합니다.
