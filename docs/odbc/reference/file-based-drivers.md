---
title: 파일 기반 드라이버 | Microsoft Docs
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
- file-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
- drivers [ODBC], file-based drivers
ms.assetid: d92e0c5c-d176-4282-bbe1-d449e2223d50
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e8ce91d6606501d64702c27c6f4915b3ec96b936
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915048"
---
# <a name="file-based-drivers"></a>파일 기반 드라이버
파일 기반 드라이버는 드라이버에 대 한 독립 실행형 데이터베이스 엔진을 제공 하지 않는 dBASE 등의 데이터 원본에 사용 됩니다. 이러한 드라이버는 실제 데이터에 직접 액세스 및는 데이터베이스 엔진의 SQL 문 처리할을 구현 해야 합니다. 표준 방법으로 파일 기반 드라이버에서 데이터베이스 엔진 구현 되는 최소 SQL 규칙 수준;에 정의 된 ODBC SQL의 하위 집합 이 규칙 수준에서 SQL 문 목록은 참조 [부록 c: SQL 문법을](../../odbc/reference/appendixes/appendix-c-sql-grammar.md)합니다.  
  
 비교 파일 및 DBMS 기반 드라이버의 파일 기반 드라이버는 네트워크 부분이 없음이 있기 때문에 구성 하려면 덜 복잡 하 게 데이터베이스 엔진 구성 인해를 작성 하기 쉽다는 점 및 성능이 낮은 사용자가 거의 없는 데이터베이스를 쓸 수 있는 시간 때문에 타사 데이터베이스에서 생성 하는 것 만큼 강력한 엔진입니다.  
  
 다음 그림에는 네트워크 파일 서버에 파일 기반 드라이버, 하나는 데이터가 있는 로컬 및 구문이 있는 다른의 서로 다른 두 구성을 보여 줍니다.  
  
 ![파일의 두 가지 구성&#45;드라이버 기반](../../odbc/reference/media/pr06.gif "pr06")
