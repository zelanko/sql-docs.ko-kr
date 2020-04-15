---
title: SQL테이블 (비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5467fc8c1717d5ceb548b3950a0894fd2a1b4499
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299289"
---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함되어 있습니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 지원: 전체  
  
 ODBC API 적합성: 레벨 1  
  
 SQLTables 문의 매개 변수에 의해 지정 된 테이블 이름 목록을 반환 **합니다.** 매개 변수를 지정하지 않으면 현재 데이터 원본에 저장된 테이블 이름을 반환합니다. 드라이버는 결과 집합으로 정보를 반환합니다.  
  
 열거 형 호출은 원격 보기 또는 로컬 매개 변수뷰에 대한 결과 집합 항목을 수신하지 않습니다. 그러나 고유한 테이블 이름 지정기를 사용하여 **SQLTables를** 호출하면 해당 이름이 있는 경우 해당 뷰에 대한 일치 항목이 검색됩니다. 이렇게 하면 새 테이블을 만들기 전에 API를 사용하여 이름 충돌을 확인할 수 있습니다.  
  
> [!NOTE]  
>  Visual FoxPro ODBC 드라이버는 두 유형의 테이블이 시스템의 동일한 디렉터리에 저장되어 있는 경우에도 [데이터베이스 테이블과](../../odbc/microsoft/visual-foxpro-terminology.md) [사용 중인 테이블을](../../odbc/microsoft/visual-foxpro-terminology.md)구분합니다. 데이터 원본이 사용 중인 테이블의 디렉토리인 경우 Visual FoxPro ODBC 드라이버는 데이터베이스와 연결된 테이블의 이름을 카탈로그화하거나 반환하지 않습니다.  
  
 자세한 내용은 *ODBC 프로그래머의 참조에서* [SQLTable을](../../odbc/reference/syntax/sqltables-function.md) 참조하십시오.
