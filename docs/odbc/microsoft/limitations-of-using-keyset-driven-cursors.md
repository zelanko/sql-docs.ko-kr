---
title: 키 집합 커서 사용에 대 한 제한 사항 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0c35f900faf1a30788b3642af3fdd65d672951d5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68054125"
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>키 집합 커서 사용 제한 사항
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 쿼리 하는 테이블에 대해 단일 ROWID 열을 검색할 수 있어야 합니다. 키 집합 커서는 DISTINCT, GROUP BY, UNION, INTERSECT 또는 빼기 절이 포함 된 조인, 쿼리 또는 문에 사용할 수 없습니다.  
  
 또한 응용 프로그램에서 테이블 별칭을 사용 하는 경우 키 집합 커서는 작동 하지 않습니다. 앞 으로만 이동 가능한 커서 유형이 나 정적 커서 유형이 필요 합니다. 테이블 별칭과 함께 키 집합 커서 유형을 사용 하면 다음 오류가 발생 합니다. "[Microsoft] [ODBC driver for Oracle] 조인에서 키 집합 커서를 사용할 수 없습니다. union, intersect 또는 마이너스 또는에서 읽기 전용 결과 집합을 사용 합니다.  
  
> [!NOTE]  
>  Oracle 서버에 전송 되는 SQL 문을 드라이버가 처리 하는 방식 때문에 Oracle은 내부적으로 다음 오류 메시지를 반환 합니다. "ORA-00964: 테이블 이름이 not in list"
