---
title: 키 집합 커서를 사용 하 여의 제한 사항 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], cursors
- keyset-driven cursors [ODBC]
ms.assetid: 59d86fed-387c-4719-9550-36343e74da44
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a8ae5c5fbc73ff0128eb44944d5a0e5573c5b0d3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>키 집합 커서를 사용 하 여의 제한 사항
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. Oracle에서 제공 하는 ODBC 드라이버를 사용 하십시오.  
  
 쿼리 테이블에 대 한 단일 행 ID 열을 검색할 수 있어야 합니다. 조인, 쿼리 또는 DISTINCT를 GROUP BY, UNION, INTERSECT를 포함 하는 문 또는 절 빼기 키 집합 커서를 사용할 수 없습니다.  
  
 또한 테이블 별칭을 사용 하 여 응용 프로그램에는 키 집합 커서 작동 하지 않습니다. 앞 으로만 이동 가능한 또는 정적 커서 유형은 필수입니다. 키 집합을 사용 하 여 테이블 별칭으로 커서 유형을 하면 다음 오류: "[Microsoft] [ODBC driver for Oracle] 키 집합 커서를 사용할 수 없습니다, 조인 된 union, intersect 또는 빼기 또는 읽기 전용 결과 집합입니다."  
  
> [!NOTE]  
>  드라이버에서 Oracle 서버에 전송 하는 SQL 문을 처리 하는 방식 때문에 Oracle 내부적으로 다음 오류 메시지가 반환: "또는 00964: 테이블 목록에 없는 이름입니다."
