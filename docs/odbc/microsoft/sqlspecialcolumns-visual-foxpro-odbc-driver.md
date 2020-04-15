---
title: SQL스페셜칼럼(비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b72a978d-6a60-475a-b7d9-c424d77bbe30
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96b439674c8bda3494b4cefd0c1118602b537cd0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299383"
---
# <a name="sqlspecialcolumns-visual-foxpro-odbc-driver"></a>SQLSpecialColumns(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함되어 있습니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 지원: 전체  
  
 ODBC API 적합성: 레벨 1  
  
 테이블의 행을 고유하게 식별하는 최적의 열 집합을 검색합니다.  
  
 Visual FoxPro ODBC 드라이버는 FoxPro 테이블의 기본 키를 구성하는 열을 반환합니다. [(SQLPrimary키](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md)를 참조하십시오.) *fColType을* 사용하여 SQL_ROWVER 호출하면 열이 반환되지 않습니다. **SQLSpecialColumns는** 데이터베이스인 데이터 원본에만 [작동합니다.](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
 자세한 내용은 *ODBC 프로그래머의 참조에서* [SQLSpecialColumns를](../../odbc/reference/syntax/sqlspecialcolumns-function.md) 참조하십시오.
