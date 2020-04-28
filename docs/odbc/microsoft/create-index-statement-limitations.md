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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 053287d5087b377429221c31dd4e6b20f24248e5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280884"
---
# <a name="create-index-statement-limitations"></a>CREATE INDEX 문 제한 사항
Microsoft Excel 또는 텍스트 드라이버에는 CREATE INDEX 문이 지원 되지 않습니다.  
  
 인덱스는 최대 10 개 열에 정의할 수 있습니다. CREATE INDEX 문에 열이 10 개 이상 포함 되어 있으면 인덱스가 인식 되지 않고 인덱스가 생성 되지 않은 것으로 간주 됩니다.  
  
 DBASE 드라이버는 논리적 열에 인덱스를 만들 수 없습니다.  
  
 DBASE 드라이버를 사용 하는 경우 SELECT 문의 WHERE 절에 지정 된 열 (필드)에 대해. x x x () 인덱스를 작성 하 여 많은 파일에 대 한 응답 시간을 향상 시킬 수 있습니다. 기존. mdx 인덱스는 WHERE 절에 있는 =, >, \<, >=, =< 및 BETWEEN 연산자와 LIKE 조건자 및 join 조건자에 자동으로 적용 됩니다.  
  
 DBASE 드라이버를 사용 하는 경우 CREATE UNIQUE INDEX 문에 의해 생성 된 인덱스는 실제로 고유 하지 않으며 인덱싱된 열에 중복 값을 삽입할 수 있습니다. 동일한 키 값을 가진 집합의 한 레코드만 인덱스에 추가할 수 있습니다.  
  
 Paradox 드라이버를 사용 하는 경우 첫 번째 열을 포함 하 여 테이블에 있는 열의 연속 하위 집합에 대해 고유 인덱스를 정의 해야 합니다. 테이블에 고유 인덱스가 정의 되어 있지 않거나 Borland 데이터베이스 엔진를 구현 하지 않고 Paradox 드라이버를 사용 하는 경우에는 Paradox 드라이버를 사용 하 여 테이블을 업데이트할 수 없습니다.
