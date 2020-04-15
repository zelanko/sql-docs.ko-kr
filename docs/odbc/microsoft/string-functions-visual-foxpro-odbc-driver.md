---
title: 문자열 함수(비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC string functions [ODBC]
- string functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], string functions
- FoxPro ODBC driver [ODBC], string functions
ms.assetid: 1974fd26-ef0d-45d5-860b-298917c8e9c3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 988ba23b95f6b138148b1fa17ad303d7aa2dc895
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299193"
---
# <a name="string-functions-visual-foxpro-odbc-driver"></a>문자열 함수(Visual FoxPro ODBC 드라이버)
다음 표에는 Visual FoxPro ODBC 드라이버에서 지원하는 ODBC 문자열 조작 기능이 나열되어 있습니다. 동일한 함수에 대한 Visual FoxPro 문법이 ODBC 구문과 다를 때 Visual FoxPro 와 동등한 문법이 나열됩니다.  
  
|ODBC 문법|비주얼 폭스프로 문법|  
|------------------|---------------------------|  
|아시이 *(string_exp)*|ASC *(string_exp)*|  
|CHAR *(코드)*|CHR *(string_exp)*|  
|CONCAT *(string_exp1, string_exp2)*|*string_exp1 + string_exp2*|  
|차이 *(string_exp1, string_exp2)*||  
|*삽입(string_exp1, 시작, 길이, string_exp2)*|물건 *(string_exp1, 시작, 길이, string_exp2)*|  
|LCASE *(string_exp)*|로어 *(string_exp)*|  
|*왼쪽(string_exp, 개수)*||  
|*길이(string_exp)*|렌 *(string_exp)*|  
|LTRIM *(string_exp)*||  
|*반복(string_exp, 개수)*|*복제(string_exp, 개수)*|  
|*교체(string_exp1, string_exp2, string_exp3)*|스트트란 *(string_exp1, string_exp2, string_exp3)*|  
|*오른쪽(string_exp, 개수)*||  
|RTRIM *(string_exp)*||  
|사운드엑스 *(string_exp)*||  
|*공백(개수)*||  
|*서브스트링(string_exp, 시작, 길이)*|SUBSTR *(string_exp, 시작, 길이)*|  
|UCASE *(string_exp)*|*어퍼(string_exp)*|
