---
description: 파일 기반 드라이버
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 770e8560c540e8423aebf0a79c0e8ee5c124c8e3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429085"
---
# <a name="file-based-drivers"></a>파일 기반 드라이버
파일 기반 드라이버는 드라이버를 사용할 수 있는 독립 실행형 데이터베이스 엔진을 제공 하지 않는 dBASE와 같은 데이터 원본에 사용 됩니다. 이러한 드라이버는 물리적 데이터에 직접 액세스 하 고 SQL 문을 처리 하기 위해 데이터베이스 엔진을 구현 해야 합니다. 표준 사례로, 파일 기반 드라이버의 데이터베이스 엔진은 최소 SQL 규칙 수준으로 정의 된 ODBC SQL의 하위 집합을 구현 합니다. 이 규칙 수준의 SQL 문 목록은 [부록 C: Sql 문법](../../odbc/reference/appendixes/appendix-c-sql-grammar.md)을 참조 하세요.  
  
 파일 기반 드라이버와 DBMS 기반 드라이버를 비교할 때 파일 기반 드라이버는 데이터베이스 엔진 구성 요소 때문에 쓰기 하기가 더 어렵고, 네트워크 부분이 없어 구성 하기가 복잡 하며, 사용자가 데이터베이스 회사에서 생성 하는 것과 강력 하 게 데이터베이스 엔진을 작성할 수 있기 때문에 더 강력 하지 않습니다.  
  
 다음 그림은 데이터를 로컬로 저장 하는 파일 기반 드라이버의 두 가지 구성과 네트워크 파일 서버에 상주 하는 파일을 보여 줍니다.  
  
 ![파일&#45;기반 드라이버의 두 가지 구성](../../odbc/reference/media/pr06.gif "pr06")
