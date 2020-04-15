---
title: 키집합 기반 커서 사용의 제한 사항 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], cursors
- keyset-driven cursors [ODBC]
ms.assetid: 59d86fed-387c-4719-9550-36343e74da44
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2aeb5a0c50192118dfff8ed7d866c3911c2b4007
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284153"
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>키 집합 커서 사용 제한 사항
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 오라클에서 제공하는 ODBC 드라이버를 사용합니다.  
  
 쿼리된 테이블에 대한 단일 ROWID 열을 검색할 수 있어야 합니다. 키집합 기반 커서는 고유, 그룹 BY, UNION, INTERSECT 또는 MINUS 절을 포함하는 조인, 쿼리 또는 문을 사용할 수 없습니다.  
  
 또한 응용 프로그램에서 테이블 별칭을 사용하는 경우 키 집합 기반 커서가 작동하지 않습니다. 정방향 전용 또는 정적 커서 유형이 필요합니다. 테이블 별칭이 있는 키집합 커서 유형을 사용하면 "[Microsoft][오라클용 ODBC 드라이버]가 결합, 교차 또는 마이너스 또는 읽기 전용 결과 집합에서 키집합 기반 커서를 사용할 수 없습니다."  
  
> [!NOTE]  
>  드라이버가 Oracle 서버로 전송되는 SQL 문을 처리하는 방식 때문에 Oracle은 내부적으로 "ORA-00964: FROM 목록에 없는 테이블 이름"이라는 오류 메시지를 반환합니다.
