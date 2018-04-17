---
title: 문자열 함수 (Visual FoxPro ODBC 드라이버) | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- ODBC string functions [ODBC]
- string functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], string functions
- FoxPro ODBC driver [ODBC], string functions
ms.assetid: 1974fd26-ef0d-45d5-860b-298917c8e9c3
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 482c21b4c9f872490ac9a2d36165fdc3fc9d8246
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="string-functions-visual-foxpro-odbc-driver"></a>문자열 함수 (Visual FoxPro ODBC 드라이버)
다음 표에서; Visual FoxPro ODBC 드라이버에서 지 원하는 ODBC 문자열 조작 함수를 보여 줍니다. Visual FoxPro 문법 동일한 기능에 대 한 ODBC 구문을 다를 경우 해당 Visual FoxPro 나열 됩니다.  
  
|ODBC 문법|Visual FoxPro 문법|  
|------------------|---------------------------|  
|ASCII *(string_exp)*|ASC *(string_exp)*|  
|CHAR *(코드)*|CHR *(string_exp)*|  
|CONCAT *(string_exp1, string_exp2)*|*string_exp1 + string_exp2*|  
|차이 *(string_exp1, string_exp2)*||  
|삽입 *(string_exp1, 시작, 길이, string_exp2)*|STUFF *(string_exp1, 시작, 길이, string_exp2)*|  
|LCASE *(string_exp)*|더 낮은 *(string_exp)*|  
|왼쪽 *(string_exp count)*||  
|길이 *(string_exp)*|LEN *(string_exp)*|  
|LTRIM *(string_exp)*||  
|반복 *(string_exp count)*|복제 *(string_exp count)*|  
|대체 *(string_exp1, string_exp2, string_exp3)*|STRTRAN *(string_exp1, string_exp2, string_exp3)*|  
|오른쪽 *(string_exp count)*||  
|RTRIM *(string_exp)*||  
|SOUNDEX *(string_exp)*||  
|공간 *(개수)*||  
|부분 문자열 *(string_exp, 시작, 길이)*|SUBSTR *(string_exp, 시작, 길이)*|  
|UCASE *(string_exp)*|위 *(string_exp)*|
