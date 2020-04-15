---
title: 파일 기반 드라이버 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- file-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
- drivers [ODBC], file-based drivers
ms.assetid: d92e0c5c-d176-4282-bbe1-d449e2223d50
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 223bd838754f1d656ac71ae37926389097af3ea1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306666"
---
# <a name="file-based-drivers"></a>파일 기반 드라이버
파일 기반 드라이버는 드라이버가 사용할 독립 실행형 데이터베이스 엔진을 제공하지 않는 dBASE와 같은 데이터 원본과 함께 사용됩니다. 이러한 드라이버는 물리적 데이터에 직접 액세스하며 SQL 문을 처리하기 위해 데이터베이스 엔진을 구현해야 합니다. 표준 사례로 파일 기반 드라이버의 데이터베이스 엔진은 최소 SQL 준수 수준으로 정의된 ODBC SQL의 하위 집합을 구현합니다. 이 준수 수준에서 SQL 문 목록은 [부록 C: SQL 문법](../../odbc/reference/appendixes/appendix-c-sql-grammar.md)을 참조하십시오.  
  
 파일 기반 드라이버와 DBMS 기반 드라이버를 비교할 때 파일 기반 드라이버는 데이터베이스 엔진 구성 요소로 인해 쓰기가 어렵고 네트워크 조각이 없기 때문에 구성하기가 덜 복잡하며 데이터베이스 회사에서 생산한 드라이버만큼 강력한 데이터베이스 엔진을 작성할 시간이 거의 없기 때문에 구성하기가 어렵습니다.  
  
 다음 그림에서는 데이터가 로컬에 상주하고 다른 하나는 네트워크 파일 서버에 상주하는 파일 기반 드라이버의 두 가지 구성을 보여 주십습니다.  
  
 ![파일&#45;기반 드라이버의 두 가지 구성](../../odbc/reference/media/pr06.gif "pr06")
