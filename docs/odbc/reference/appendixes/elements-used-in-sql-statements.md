---
title: SQL 문에서 사용 되는 요소 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], elements supported
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 85777525-1555-4731-8309-63a464c6b43a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e33beff29463172a26d53953dd5f563fe1f3f5c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240961"
---
# <a name="elements-used-in-sql-statements"></a>SQL 문에 사용되는 요소
다음 요소는 이전에 나열 된 SQL 문에서 사용 됩니다.  
  
## <a name="element"></a>요소  
 *base-table-identifier* ::= *user-defined-name*  
  
 *base-table-name* ::= *base-table-identifier*  
  
 *부울 인수* :: [NOT] = *부울 주*  
  
 *boolean-primary* ::= comparison *-predicate* &#124; ( *search-condition* )  
  
 *boolean-term* ::= *boolean-factor* [AND *boolean-term*]  
  
 *character-string-literal* ::= ''{*character*}...'' (*문자* 드라이버/데이터 원본의 문자 집합의 모든 문자입니다. 리터럴 작은따옴표 문자 (") 문자 문자열 리터럴에 포함 하려면 두 개의 리터럴 따옴표 문자를 사용 하 여 [' '].)  
  
 *column-identifier* ::= *user-defined-name*  
  
 *column-name* ::= [*table-name*.]*column-identifier*  
  
 *비교 연산자* :: = < &#124; > &#124; \<= &#124; > = &#124; = &#124; <>  
  
 *비교 조건자* :: = *식* 비교 연산자 식  
  
 *데이터 형식* :: = *문자 문자열 형식* (*문자 문자열 형식* 모든 데이터 형식이 있는 SQLGetTypeInfo에서 반환한 결과 집합을 "" DATA_TYPE"" 열이 두 SQL_CHAR 또는 SQL_VARCHAR입니다.)  
  
 *digit* ::= 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9  
  
 *dynamic-parameter* ::= ?  
  
 *식을* :: 용어 = &#124; 식 {+&#124;-} 용어  
  
 *factor* ::= [*+*&#124;*-*]*primary*  
  
 *insert-value* ::=  
  
 *dynamic-parameter*  
  
 &#124;*리터럴*  
  
 &#124; NULL  
  
 &#124; USER  
  
 *문자* :: = *lower case 문자 &#124; 위 사례 편지*  
  
 *literal* ::= *character-string-literal*  
  
 *lower case 편지* :: =는 &#124; b &#124; c &#124; d &#124; 전자 &#124; f &#124; g &#124; h &#124; 있습니까 &#124; j &#124; k &#124; l &#124; m &#124; n &#124; o &#124; p &#124; q &#124; r &#124; s &#124; t &#124; u &#124; v &#124; w &#124; x &#124; y &#124; z  
  
 *order by 절* :: ORDER BY = *정렬 사양* [합니다 *정렬 사양*]...  
  
 *primary* ::= *column-name*  
  
 &#124; *dynamic-parameter*  
  
 &#124;*리터럴*  
  
 &#124;( *식* )  
  
 *search-condition* ::= *boolean-term* [OR *search-condition*]  
  
 *선택 목록* :: = \* &#124; *선택 하위 목록* [, *선택 하위 목록*]...  (*선택 목록* 매개 변수를 포함할 수 없습니다.)  
  
 *select-sublist* ::= *expression*  
  
 *정렬 사양* :: = {*부호 없는 정수 &#124; 열 이름*} [*ASC &#124; DESC*]  
  
 *table-identifier* ::= *user-defined-name*  
  
 *table-name* ::= *table-identifier*  
  
 *table-reference* ::= *table-name*  
  
 *table-reference-list* ::= *table-reference* [,*table-reference*]...  
  
 *term* ::= *factor* &#124; *term* {\*&#124;*/*} *factor*  
  
 *unsigned-integer* ::= {*digit*}  
  
 *위 사례 편지* :: = *는 &#124; B &#124; C &#124; D &#124; E &#124; F &#124; G &#124; 시간 &#124; 있습니까 &#124; J &#124; K &#124; L &#124; M &#124; N &#124; O &#124; &#124;Q &#124; R &#124; S &#124; T &#124; U &#124; V &#124; W &#124; X &#124; Y &#124; Z*  
  
 *user-defined-name* ::= *letter*[*digit* &#124; *letter* &#124; *_*]...
