---
title: 키 집합 커서를 사용 하 여의 제한 사항 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 3c4910ebd2c6dd988e937f1e9d6a3281bb0e9741
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47668111"
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>키 집합 커서 사용 제한 사항
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신, Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 쿼리 테이블에 대 한 단일 ROWID 열을 검색할 수 있어야 합니다. 조인, 쿼리 또는 DISTINCT를 GROUP BY, UNION, INTERSECT를 포함 하는 문 또는 절 빼기 키 집합 커서를 사용할 수 없습니다.  
  
 또한 테이블 별칭을 사용 하 여 응용 프로그램에는 키 집합 커서 작동 하지 않습니다. 앞 으로만 이동 가능한 또는 정적 커서 유형은 필수입니다. 키 집합을 사용 하 여 테이블 별칭을 사용 하 여 커서 유형을 하면 다음 오류: "[Microsoft] [ODBC driver for Oracle] 키 집합 커서를 사용할 수 없습니다 조인 공용 구조체를 사용 하 여 교차 또는 빼기 또는 읽기 전용 결과 집합입니다."  
  
> [!NOTE]  
>  드라이버가 Oracle 서버에 전송 되는 SQL 문을 처리 하는 방식 때문에 Oracle 내부적으로 다음 오류 메시지를 반환 합니다. "ORA-00964: 테이블 목록에 없는 이름을."
