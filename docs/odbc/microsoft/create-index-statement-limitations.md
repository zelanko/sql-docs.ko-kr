---
title: 인덱스 문에 제한 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX statement limitations [ODBC]
- ODBC SQL grammar, CREATE INDEX statement limitations
ms.assetid: 832dcda1-e452-48e6-8adb-7fb33c4fb4ff
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d473a0fce55688dfa00fd916c5eab15bd4ad44e2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="create-index-statement-limitations"></a>인덱스 문에 제한 만들기
Microsoft Excel 또는 텍스트 드라이버에 대 한 CREATE INDEX 문이 지원 되지 않습니다.  
  
 최대 10 개의 열에 인덱스를 정의할 수 있습니다. CREATE INDEX 문을에 10 개 이상의 열이 포함 하는 인덱스 인식 되지 않습니다 및 테이블 인덱스가 생성 된 것 처럼 처리 됩니다.  
  
 DBASE 드라이버 논리 열에 인덱스를 만들 수 없습니다.  
  
 DBASE 드라이버를 사용 하면 SELECT 문의 WHERE 절에 지정 된 열 (필드)에.mdx (또는.ndx) 인덱스를 작성 하 여 큰 파일에서 응답 시간이 향상 될 수 있습니다. 기존.mdx 인덱스 =에 대 한 자동 적용 됩니다 >, \<, > =, = <, 및 BETWEEN 연산자는 WHERE 절 및 LIKE 조건자, 뿐만 아니라에 조인 조건자입니다.  
  
 DBASE 드라이버를 사용 하는 CREATE UNIQUE INDEX 문에 의해 생성 된 인덱스 실제로 고유 하지 않으며 인덱싱된 열에 중복 값을 삽입할 수 있습니다. 인덱스에 동일한 키 값을 가진 집합에서 레코드를 하나만 추가할 수 있습니다.  
  
 Paradox 드라이버를 사용할 경우 인접 한 하위 집합의 첫 번째 열을 포함 하는 테이블의 열에 고유 인덱스를 정의 합니다. Borland 데이터베이스 엔진의 구현 없이 Paradox 드라이버를 사용 하거나 테이블에 고유 인덱스가 정의 되어 있지 않으면 Paradox 드라이버에서 테이블을 업데이트할 수 없습니다.
