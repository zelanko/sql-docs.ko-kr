---
title: SQLColAttributes (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: d403dfa0-c26d-47d4-91d9-2f29aa387399
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e34929315d3a3548799bc605dbb8f3c4a2f665d0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47820062"
---
# <a name="sqlcolattributes-visual-foxpro-odbc-driver"></a>SQLColAttributes(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보를 포함합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 ODBC API 규칙: 코어 수준  
  
 결과 집합의 열에 대 한 설명자 정보를 반환합니다. 설명자 정보 문자열, 32 비트 설명자 종속 값 또는 정수 값으로 반환 됩니다.  
  
> [!NOTE]  
>  **SQLColAttributes** 책갈피 열 (0)에 대 한 정보를 반환 하는데 사용할 수 없습니다.  
  
 Visual FoxPro ODBC 드라이버를 지 원하는 모든 *fDescType* 값입니다. 다음 표에서 선택한 값의 드라이버의 구현에 대 한 의견을 포함합니다.  
  
|*fDescType*|설명|  
|-----------------|-------------|  
|SQL_COLUMN_AUTO_INCREMENT|FALSE를 반환 합니다: Visual FoxPro 필드가 없습니다. 카운터입니다.|  
|SQL_COLUMN_CASE_SENSITIVE|열 유형이 문자에 항상 TRUE를 반환 합니다.|  
|SQL_COLUMN_LABEL|또한 SQL_COLUMN_NAME에서 반환 하는 열 이름을 반환 합니다.|  
|SQL_COLUMN_MONEY|열 유형입니다 (Visual FoxPro 언어에서 "Y"로 표현 됨) 통화 하는 경우 TRUE를 반환 합니다.|  
|SQL_COLUMN_OWNER_NAME|항상 빈 문자열을 반환합니다.|  
|SQL_COLUMN_QUALIFIER_NAME|항상 빈 문자열을 반환합니다.|  
|SQL_COLUMN_SEARCHABLE|일반; 형식의 열에 대 한 SQL_UNSEARCHABLE를 반환합니다. 이러한 열을 WHERE 절에서 사용할 수 없습니다.<br /><br /> 문자 또는 메모 NOCPTRANS 사용 하 여 형식의 열에 대 한 반환 SQL_SEARCHABLE 설정 되지 않은; 이러한 열은 임의의 비교 연산자를 사용 하 여 WHERE 절에서 사용할 수 있습니다.<br /><br /> 다른 모든 열 유형의; SQL_ALL_EXCEPT_LIKE 반환 이러한 열 유사 제외한 모든 비교 연산자를 사용 하 여 WHERE 절에서 사용할 수 있습니다.|  
|SQL_COLUMN_TABLE_NAME|항상 빈 문자열을 반환합니다.|  
  
 자세한 내용은 [SQLColAttributes](../../odbc/reference/syntax/sqlcolattributes-function.md) 에 *ODBC 프로그래머 참조*합니다.
