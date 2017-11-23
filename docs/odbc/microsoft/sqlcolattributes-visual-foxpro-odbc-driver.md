---
title: "SQLColAttributes (Visual FoxPro ODBC 드라이버) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLColAttribute function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: d403dfa0-c26d-47d4-91d9-2f29aa387399
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 750f95ef793d36daca117817d81f9136ef016a55
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlcolattributes-visual-foxpro-odbc-driver"></a>SQLColAttributes (Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보입니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 ODBC API 규칙: 핵심 수준  
  
 결과 집합의 열에 대 한 설명자 정보를 반환합니다. 설명자 정보 문자열, 32 비트 설명자 종속 값 또는 정수 값으로 반환 됩니다.  
  
> [!NOTE]  
>  **SQLColAttributes** 책갈피 열 (열 0)에 대 한 정보를 반환 하는 데 사용 될 수 없습니다.  
  
 Visual FoxPro ODBC 드라이버를 지 원하는 모든 *fDescType* 값입니다. 다음 표에서 선택한 값의 드라이버의 구현에 대 한 의견을 포함합니다.  
  
|*fDescType*|설명|  
|-----------------|-------------|  
|SQL_COLUMN_AUTO_INCREMENT|FALSE를 반환 합니다: Visual FoxPro 필드가 없습니다. 카운터입니다.|  
|SQL_COLUMN_CASE_SENSITIVE|항상 열 유형이 문자 이면 TRUE를 반환 합니다.|  
|SQL_COLUMN_LABEL|또한 SQL_COLUMN_NAME에서 반환 되는 열 이름을 반환 합니다.|  
|SQL_COLUMN_MONEY|열 형식이 통화 ("Y" Visual FoxPro 언어에서 표시 됨) 하는 경우 TRUE를 반환 합니다.|  
|SQL_COLUMN_OWNER_NAME|항상 빈 문자열을 반환합니다.|  
|SQL_COLUMN_QUALIFIER_NAME|항상 빈 문자열을 반환합니다.|  
|SQL_COLUMN_SEARCHABLE|일반; 형식의 열에 대 한 SQL_UNSEARCHABLE 반환 이러한 열을 WHERE 절에 사용할 수 없습니다.<br /><br /> 문자 또는 메모 NOCPTRANS와 유형의 열에 대 한 반환 SQL_SEARCHABLE 설정 하지; 이러한 열은 모든 비교 연산자와 함께 WHERE 절에 사용할 수 있습니다.<br /><br /> 다른 모든 열 유형의; SQL_ALL_EXCEPT_LIKE 반환 이러한 열은 LIKE 제외한 모든 비교 연산자가 있는 WHERE 절에 사용할 수 있습니다.|  
|SQL_COLUMN_TABLE_NAME|항상 빈 문자열을 반환합니다.|  
  
 자세한 내용은 참조 [SQLColAttributes](../../odbc/reference/syntax/sqlcolattributes-function.md) 에 *ODBC Programmer's Reference*합니다.
