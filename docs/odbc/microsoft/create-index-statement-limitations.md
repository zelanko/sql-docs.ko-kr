---
title: CREATE INDEX 문 제한 사항 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX statement limitations [ODBC]
- ODBC SQL grammar, CREATE INDEX statement limitations
ms.assetid: 832dcda1-e452-48e6-8adb-7fb33c4fb4ff
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec6ba27197f7a6021aff90d30884129128cb3614
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63232279"
---
# <a name="create-index-statement-limitations"></a>CREATE INDEX 문 제한 사항
Microsoft Excel 또는 텍스트 드라이버에 대 한 CREATE INDEX 문이 지원 되지 않습니다.  
  
 최대 10 개의 열에 인덱스를 정의할 수 있습니다. 10 개 열은 CREATE INDEX 문에 포함 하는 경우 인덱스 인식 되지 않습니다 및 테이블 인덱스가 생성 된 것 처럼 처리 됩니다.  
  
 DBASE 드라이버 논리 열에 인덱스를 만들 수 없습니다.  
  
 DBASE 드라이버를 사용 하면 SELECT 문의 WHERE 절에 지정 된 열 (필드)에서.mdx (또는.ndx) 인덱스를 작성 하 여 큰 파일의 응답 시간을 개선할 수 있습니다. 기존.mdx 인덱스 =, 자동으로 적용 됩니다 >, \<, > =, = <, 및 BETWEEN 연산자와 버전에 WHERE 절 및 LIKE 조건자에 조인 조건자입니다.  
  
 DBASE 드라이버를 사용 하는 경우 CREATE UNIQUE INDEX 문에 의해 생성 된 인덱스는 실제로 비고유, 및 인덱싱된 열에 중복 값을 삽입할 수 있습니다. 인덱스에 동일한 키 값을 사용 하 여 집합에서 레코드를 하나만 추가할 수 있습니다.  
  
 Paradox 드라이버를 사용 하는 경우 고유 인덱스를 첫 번째 열을 포함 하 여 테이블의 열 인접 한 하위 집합에 정의 되어야 합니다. Paradox 드라이버 Borland 데이터베이스 엔진의 구현 없이 사용 하는 경우 또는 테이블에 고유 인덱스가 정의 되어 있지 않으면 Paradox 드라이버에서 테이블을 업데이트할 수 없습니다.
