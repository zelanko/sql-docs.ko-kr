---
title: 문자열 함수 (Visual FoxPro ODBC 드라이버) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a9e1c94eec150cc24522cd6e4c57eb35b4a2126
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270922"
---
# <a name="string-functions-visual-foxpro-odbc-driver"></a>문자열 함수(Visual FoxPro ODBC 드라이버)
다음 표에서 Visual FoxPro ODBC 드라이버;에서 지 원하는 ODBC 문자열 조작 함수 동일한 함수에 대 한 Visual FoxPro 문법 ODBC 구문을 다를 경우에 해당 Visual FoxPro 나열 됩니다.  
  
|ODBC 문법|Visual FoxPro 문법|  
|------------------|---------------------------|  
|ASCII *(string_exp)*|ASC *(string_exp)*|  
|CHAR *(코드)*|CHR *(string_exp)*|  
|CONCAT *(string_exp1, string_exp2)*|*string_exp1 + string_exp2*|  
|DIFFERENCE *(string_exp1, string_exp2)*||  
|삽입 *(string_exp1, 시작, 길이, string_exp2)*|STUFF *(string_exp1, start, length, string_exp2)*|  
|LCASE *(string_exp)*|LOWER *(string_exp)*|  
|LEFT *(string_exp, count)*||  
|LENGTH *(string_exp)*|LEN *(string_exp)*|  
|LTRIM *(string_exp)*||  
|REPEAT *(string_exp, count)*|복제 *(string_exp를 개수)*|  
|REPLACE *(string_exp1, string_exp2, string_exp3)*|STRTRAN *(string_exp1, string_exp2, string_exp3)*|  
|RIGHT *(string_exp, count)*||  
|RTRIM *(string_exp)*||  
|SOUNDEX *(string_exp)*||  
|공간 *(개수)*||  
|부분 문자열 *(string_exp를 시작, 길이)*|SUBSTR *(string_exp, start, length)*|  
|UCASE *(string_exp)*|UPPER *(string_exp)*|
