---
title: SQLGetTypeInfo (비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5f25e20b-a4ef-42da-aeb6-00e0510fb1cc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 23db0350f0f7271f85e2bc5c6a9e6c8767443a85
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299523"
---
# <a name="sqlgettypeinfo-visual-foxpro-odbc-driver"></a>SQLGetTypeInfo(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함되어 있습니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 지원: 전체  
  
 ODBC API 적합성: 레벨 1  
  
 데이터 원본에서 지원하는 데이터 형식에 대한 정보를 반환합니다. 드라이버는 SQL 결과 집합의 정보를 반환합니다. 다음 표에는 ODBC 데이터 형식과 해당 Visual FoxPro 데이터 형식이 나열되어 있습니다.  
  
|ODBC 형식|비주얼 폭스프로 타입|  
|---------------|------------------------|  
|SQL_BIGINT|지원되지 않습니다. 64비트 Visual FoxPro 유형이 없습니다.|  
|SQL_BIT|논리|  
|SQL_CHAR|문자|  
|SQL_DATE|Date|  
|SQL_DECIMAL|숫자|  
|SQL_DOUBLE|Double|  
|SQL_FLOAT|Double|  
|SQL_INTEGER|정수|  
|SQL_LONGVARBINARY|메모 (바이너리)|  
|SQL_LONGVARCHAR|메모|  
|SQL_NUMERIC|숫자 *, 통화, 부동|  
|SQL_REAL|Double|  
|SQL_SMALLINT|정수|  
|SQL_TIME|지원되지 않습니다. 시각적 FoxPro *시간* 유형이 없습니다.|  
|SQL_TIMESTAMP|DateTime|  
|SQL_TINYINT|정수|  
|SQL_VARBINARY|메모 (바이너리)*, 일반|  
|SQL_VARCHAR|문자|  
  
 *기본 유형  
  
 Visual FoxPro 데이터 형식에 대한 자세한 내용은 [테이블 만들기](../../odbc/microsoft/create-table-sql-command.md)를 참조하십시오. 이 함수에 대한 자세한 내용은 *ODBC 프로그래머 의 참조에서* [SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md) 를 참조하십시오.
