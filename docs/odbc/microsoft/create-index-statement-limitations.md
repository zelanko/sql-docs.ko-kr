---
title: 인덱스 명령문 제한 사항 만들기 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280884"
---
# <a name="create-index-statement-limitations"></a>CREATE INDEX 문 제한 사항
만들기 INDEX 문은 Microsoft Excel 또는 텍스트 드라이버에 대해 지원되지 않습니다.  
  
 인덱스는 최대 10개의 열에서 정의할 수 있습니다. CREATE INDEX 문에 10개 이상의 열이 포함된 경우 인덱스가 인식되지 않으며 테이블은 인덱스가 생성되지 않은 것처럼 처리됩니다.  
  
 dBASE 드라이버는 논리 열에 인덱스를 만들 수 없습니다.  
  
 dBASE 드라이버를 사용하면 SELECT 문의 WHERE 절에 지정된 열(필드)에 .mdx(또는 .ndx) 인덱스를 작성하여 대용량 파일의 응답 시간을 향상시킬 수 있습니다. 기존 .mdx 인덱스는 WHERE 절의 =, \<>, >= = =< 및 WHERE 절의 연산자 간 및 LIKE 조건자뿐만 아니라 조인 조건자에도 자동으로 적용됩니다.  
  
 dBASE 드라이버를 사용하면 고유 인덱스 만들기 문으로 만든 인덱스가 실제로 고유하지 않으며 중복 값을 인덱싱된 열에 삽입할 수 있습니다. 동일한 키 값을 가진 집합의 레코드 하나만 인덱스에 추가할 수 있습니다.  
  
 역설 드라이버를 사용할 때 첫 번째 열을 포함하여 테이블의 연속된 열 하위 집합에 대해 고유한 인덱스를 정의해야 합니다. 테이블에 고유한 인덱스가 정의되지 않았거나 Borland 데이터베이스 엔진을 구현하지 않고 역설 드라이버를 사용하는 경우 패러독스 드라이버에서 테이블을 업데이트할 수 없습니다.
