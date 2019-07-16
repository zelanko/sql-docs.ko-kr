---
title: SQLTables (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTables function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 69e2a038-5def-423f-91aa-8756e069dd2a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22e5f34a6accac3a2bb0d1ecefe7c1d5431cb562
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949003"
---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보를 포함합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 ODBC API 규칙: 수준 1  
  
 매개 변수에서 지정한 테이블 이름 목록을 반환 합니다 **SQLTables** 문입니다. 없는 매개 변수를 지정 하는 경우에 현재 데이터 원본에 저장 된 테이블 이름을 반환 합니다. 드라이버 정보 결과 집합으로 반환 합니다.  
  
 열거형 형식 호출에는 원격 뷰 또는 로컬 매개 변수가 있는 뷰에 대 한 결과 집합 항목을 수신 하지 않습니다. 그러나 호출 **SQLTables** 고유 테이블이 포함 된 이름이 있는 경우 이름 지정자 이러한 보기에 대 한 일치 하는 것은 이렇게 하면 새 테이블을 만들기 전에 이름 충돌을 확인 하는 데 사용할 API입니다.  
  
> [!NOTE]  
>  Visual FoxPro ODBC 드라이버를 구별 [데이터베이스 테이블](../../odbc/microsoft/visual-foxpro-terminology.md) 하 고 [테이블 무료](../../odbc/microsoft/visual-foxpro-terminology.md)양쪽 테이블의 시스템에서 동일한 디렉터리에 저장 됩니다 하는 경우에 합니다. 데이터 원본에 사용 가능한 테이블 디렉터리 이면 Visual FoxPro ODBC 드라이버 카탈로그 또는 데이터베이스와 연결 된 모든 테이블의 이름을 반환 하지 않습니다.  
  
 자세한 내용은 [SQLTables](../../odbc/reference/syntax/sqltables-function.md) 에 *ODBC 프로그래머 참조*합니다.
