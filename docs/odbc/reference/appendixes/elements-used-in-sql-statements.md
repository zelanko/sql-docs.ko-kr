---
title: SQL 문에 사용 되는 요소 | Microsoft Docs
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
ms.openlocfilehash: caf8f68221c1ac14649bf10be0105e1e691c7482
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68129963"
---
# <a name="elements-used-in-sql-statements"></a>SQL 문에 사용되는 요소
다음 요소는 앞에 나열 된 SQL 문에서 사용 됩니다.  
  
## <a name="element"></a>요소  
 *기본 테이블-식별자* :: = *사용자 정의 이름*  
  
 *기본 테이블-이름* :: = *기본-테이블-식별자*  
  
 *부울-factor* :: = [NOT] *boolean-기본*  
  
 *부울-primary* :: = comparison *-조건자* &#124; ( *검색 조건* )  
  
 *부울 term* :: = *부울 요소* [및 *부울 기간*]  
  
 *문자 문자열-리터럴* :: = ' ' {*character*} ... ' ' *문자* 는 드라이버/데이터 원본의 문자 집합에 있는 모든 문자입니다. 문자 문자열 리터럴에 단일 리터럴 따옴표 문자 (' ')를 포함 하려면 두 개의 리터럴 따옴표 문자 [' ' ' ']를 사용 합니다.  
  
 *열 식별자* :: = *사용자 정의 이름*  
  
 *열 이름* :: = [*테이블 이름*.] *열 식별자*  
  
 *비교-operator* :: = < &#124; > &#124; \<= &#124; >= &#124; = &#124; <>  
  
 *비교-조건자* :: = *식* 비교 연산자 식  
  
 *데이터 형식* :: = *문자열* 형식 (SQLGetTypeInfo는 반환 되는 결과 집합의 "" DATA_TYPE "" 열이 SQL_CHAR 또는 SQL_VARCHAR 인 데이터*형식입니다.* )  
  
 *digit* :: = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9  
  
 *동적-매개 변수* :: =?  
  
 *expression* :: = term &#124; expression {+&#124;-} term  
  
 *factor* :: = [*+*&#124;*-*]*기본*  
  
 *삽입 값* :: =  
  
 *동적 매개 변수*  
  
 &#124; *리터럴*  
  
 NULL &#124;  
  
 사용자 &#124;  
  
 *letter* :: = 소문자 *&#124; 대문자* (대문자)  
  
 *literal* :: = *문자-문자열 리터럴*  
  
 *소문자* :: = a &#124; b &#124; c &#124; d &#124; e &#124; f &#124; g &#124; h &#124; i &#124; j &#124; k &#124; l &#124; m &#124; n &#124; o &#124; p &#124; q &#124; r &#124; s &#124; t &#124; u &#124; v &#124; w &#124; x &#124; y &#124; z  
  
 *order by 절* :: = order BY *정렬* 기준 [, *정렬 사양*] ...  
  
 *primary* :: = *열 이름*  
  
 &#124; *동적 매개 변수*  
  
 &#124; *리터럴*  
  
 &#124; ( *식* )  
  
 *검색 조건* :: = *부울 용어* [또는 *검색 조건*]  
  
 *select-list* :: = \* &#124; *select-* 하위 목록 [, *선택-* 하위 목록] ...  (*select-list* 는 매개 변수를 포함할 수 없습니다.)  
  
 *select-하위 목록* :: = *식*  
  
 *정렬 사양* :: = {*unsigned-integer &#124; 열 이름*} [*ASC &#124; DESC*]  
  
 *테이블-identifier* :: = *사용자 정의 이름*  
  
 *테이블-이름* :: = *테이블-식별자*  
  
 *테이블-reference* :: = *table-name*  
  
 *테이블-참조-목록* :: = *테이블-참조* [,*테이블 참조*] ...  
  
 *term* :: = *factor* &#124; *term* {\*&#124;*/*} *factor*  
  
 *unsigned-integer* :: = {*digit*}  
  
 *대문자* :: = *A &#124; B &#124; C &#124; D &#124; E &#124; F &#124; G &#124; H &#124; I &#124; J &#124; K &#124; L &#124; M &#124; N &#124; O &#124; P &#124; Q &#124; R &#124; S &#124; T &#124; U &#124; V &#124; W &#124; X &#124; Y &#124; Z*  
  
 *사용자 정의 이름* :: = *letter*[*숫자* &#124; *문자* &#124; *_*] ...
