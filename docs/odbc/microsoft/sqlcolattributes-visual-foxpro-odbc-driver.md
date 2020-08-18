---
description: SQLColAttributes(Visual FoxPro ODBC 드라이버)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 062a5af2e8aab4d71cf201284bd065242c588f6a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412199"
---
# <a name="sqlcolattributes-visual-foxpro-odbc-driver"></a>SQLColAttributes(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함 되어 있습니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 지원: 전체  
  
 ODBC API 규칙: 코어 수준  
  
 결과 집합의 열에 대 한 설명자 정보를 반환 합니다. 설명자 정보는 문자열, 32 비트 설명자 종속 값 또는 정수 값으로 반환 됩니다.  
  
> [!NOTE]  
>  **Sqlcolattributes** 는 책갈피 열 (열 0)에 대 한 정보를 반환 하는 데 사용할 수 없습니다.  
  
 Visual FoxPro ODBC 드라이버는 모든 *fDescType* 값을 지원 합니다. 다음 표에는 선택한 값의 드라이버 구현에 대 한 주석이 포함 되어 있습니다.  
  
|*fDescType*|의견|  
|-----------------|-------------|  
|SQL_COLUMN_AUTO_INCREMENT|FALSE를 반환 합니다. Visual FoxPro에 카운터 필드가 없습니다.|  
|SQL_COLUMN_CASE_SENSITIVE|열 형식이 문자인 경우 항상 TRUE를 반환 합니다.|  
|SQL_COLUMN_LABEL|SQL_COLUMN_NAME에 의해 반환 되는 열 이름을 반환 합니다.|  
|SQL_COLUMN_MONEY|열 형식이 통화 (Visual FoxPro 언어의 "Y"로 나타냄) 인 경우 TRUE를 반환 합니다.|  
|SQL_COLUMN_OWNER_NAME|항상 빈 문자열을 반환합니다.|  
|SQL_COLUMN_QUALIFIER_NAME|항상 빈 문자열을 반환합니다.|  
|SQL_COLUMN_SEARCHABLE|일반 형식의 열에 대 한 SQL_UNSEARCHABLE를 반환 합니다. 이러한 열은 WHERE 절에서 사용할 수 없습니다.<br /><br /> NOCPTRANS 집합이 설정 되지 않은 문자 또는 메모 형식의 열에 대 한 SQL_SEARCHABLE를 반환 합니다. 이러한 열은 비교 연산자와 함께 WHERE 절에서 사용할 수 있습니다.<br /><br /> 다른 모든 열 형식에 대 한 SQL_ALL_EXCEPT_LIKE를 반환 합니다. 이러한 열은 LIKE를 제외한 모든 비교 연산자와 함께 WHERE 절에서 사용할 수 있습니다.|  
|SQL_COLUMN_TABLE_NAME|항상 빈 문자열을 반환합니다.|  
  
 자세한 내용은 *ODBC 프로그래머 참조*의 [sqlcolattributes](../../odbc/reference/syntax/sqlcolattributes-function.md) 를 참조 하십시오.
