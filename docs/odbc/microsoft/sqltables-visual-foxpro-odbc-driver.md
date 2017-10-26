---
title: "SQLTables (Visual FoxPro ODBC 드라이버) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLTables function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 69e2a038-5def-423f-91aa-8756e069dd2a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fd3e59437eae02a94353a6205e567fde208f4b97
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables (Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보입니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 수준 1 ODBC API 적용:  
  
 매개 변수에서 지정한 테이블 이름 목록을 반환 하는 **SQLTables** 문. 없는 매개 변수를 지정 하는 경우 현재 데이터 원본에 저장 된 테이블 이름을 반환 합니다. 드라이버 정보 결과 집합으로 반환 합니다.  
  
 열거형 형식 호출 원격 뷰 또는 로컬 매개 변수화 된 보기에 대 한 결과 집합 항목을 수신 하지 않습니다. 그러나에 대 한 호출 **SQLTables** 고유 테이블이 포함 된 이름이 있는 경우 이름 지정자 이러한 보기에 대 한 일치를 찾으려고 합니다; 이렇게 하면 새 테이블의 이전 이름 충돌을 확인 하는 데 사용할 API입니다.  
  
> [!NOTE]  
>  Visual FoxPro ODBC 드라이버를 구분 [데이터베이스 테이블](../../odbc/microsoft/visual-foxpro-terminology.md) 및 [테이블 있음](../../odbc/microsoft/visual-foxpro-terminology.md)두 유형 모두 테이블의 시스템에 동일한 디렉터리에 저장 된 경우에, 합니다. 데이터 원본에 사용 가능한 테이블 디렉터리 이면 Visual FoxPro ODBC 드라이버 카탈로그 하거나 데이터베이스와 관련 된 모든 테이블의 이름을 반환 하지 않습니다.  
  
 자세한 내용은 참조 [SQLTables](../../odbc/reference/syntax/sqltables-function.md) 에 *ODBC Programmer's Reference*합니다.

