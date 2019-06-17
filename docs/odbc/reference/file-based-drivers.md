---
title: 파일 기반 드라이버 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45d9203a08b9c70809e81fb3d9cf84a521017068
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62628605"
---
# <a name="file-based-drivers"></a>파일 기반 드라이버
파일 기반 드라이버는 드라이버 사용에 대 한 독립 실행형 데이터베이스 엔진을 제공 하지 않는 dBASE와 같은 데이터 원본 사용 됩니다. 이러한 드라이버는 실제 데이터에 직접 액세스 및 SQL 문 처리할 하는 데이터베이스 엔진을 구현 해야 합니다. 파일 기반 드라이버에서 데이터베이스 엔진을 표준 사례로 최소 SQL 적합성 수준에서 정의 하는 ODBC SQL의 하위 집합을 구현 이 규칙 수준에서 SQL 문의 목록을 참조 하세요. [부록 c: SQL 문법을](../../odbc/reference/appendixes/appendix-c-sql-grammar.md)합니다.  
  
 비교 파일 및 DBMS 기반 드라이버의 파일 기반 드라이버는 데이터베이스 엔진 구성 요소에 구성 되므로 네트워크 부분이 없음을 덜 복잡 하 게 인해 작성 하기가 및 덜 강력한 소수의 사용자가 데이터베이스를 쓸 수 있는 시간 때문에 타사 데이터베이스에서 생성 된 것으로 강력한 엔진입니다.  
  
 다음 그림은 네트워크 파일 서버의 파일 기반 드라이버, 하나는 데이터를 로컬로 상주 및 상주 하는 다른 두 개의 다른 구성을 보여 줍니다.  
  
 ![파일의 두 가지 구성&#45;기반 드라이버](../../odbc/reference/media/pr06.gif "pr06")
