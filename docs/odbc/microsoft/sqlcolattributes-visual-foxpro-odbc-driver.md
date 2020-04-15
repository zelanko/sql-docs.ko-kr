---
title: SQLColAttributes (비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
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
ms.openlocfilehash: 9508fa7b9ada8273e1250d7584e577892acf5c51
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307914"
---
# <a name="sqlcolattributes-visual-foxpro-odbc-driver"></a>SQLColAttributes(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함되어 있습니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 지원: 전체  
  
 ODBC API 적합성: 코어 레벨  
  
 결과 집합의 열에 대한 설명자 정보를 반환합니다. 설명자 정보는 문자 문자열, 32비트 설명자 종속 값 또는 정수 값으로 반환됩니다.  
  
> [!NOTE]  
>  **SQLColAttributes는** 책갈피 열(열 0)에 대한 정보를 반환하는 데 사용할 수 없습니다.  
  
 Visual FoxPro ODBC 드라이버는 모든 *fDescType* 값을 지원합니다. 다음 표에는 선택한 값의 드라이버 구현에 대한 주석이 포함되어 있습니다.  
  
|*fDescType*|주석|  
|-----------------|-------------|  
|SQL_COLUMN_AUTO_INCREMENT|FALSE 반환: Visual FoxPro에 카운터 필드가 없습니다.|  
|SQL_COLUMN_CASE_SENSITIVE|열 유형이 문자인 경우 항상 TRUE를 반환합니다.|  
|SQL_COLUMN_LABEL|SQL_COLUMN_NAME 반환되는 열 이름을 반환합니다.|  
|SQL_COLUMN_MONEY|열 유형이 통화인 경우 TRUE를 반환합니다(Visual FoxPro 언어에서 "Y"로 표시).|  
|SQL_COLUMN_OWNER_NAME|항상 빈 문자열을 반환합니다.|  
|SQL_COLUMN_QUALIFIER_NAME|항상 빈 문자열을 반환합니다.|  
|SQL_COLUMN_SEARCHABLE|일반 형식의 열에 대한 SQL_UNSEARCHABLE 반환합니다. 이러한 열은 WHERE 절에서 사용할 수 없습니다.<br /><br /> NOCPTRANS가 설정되지 않은 문자 또는 메모 형식의 열에 대한 SQL_SEARCHABLE 반환합니다. 이러한 열은 모든 비교 연산자가 있는 WHERE 절에서 사용할 수 있습니다.<br /><br /> 다른 모든 열 형식에 대해 SQL_ALL_EXCEPT_LIKE 반환합니다. 이러한 열은 LIKE를 제외한 모든 비교 연산자가 있는 WHERE 절에서 사용할 수 있습니다.|  
|SQL_COLUMN_TABLE_NAME|항상 빈 문자열을 반환합니다.|  
  
 자세한 내용은 *ODBC 프로그래머의 참조에서* [SQLColAttributes를](../../odbc/reference/syntax/sqlcolattributes-function.md) 참조하십시오.
