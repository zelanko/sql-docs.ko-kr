---
title: 드라이버 작업 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], tasks
ms.assetid: 184c795a-c2e8-4d20-9902-12e60b2f0e45
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e2ed50ac3f9e914953abdd64907199a5f978af2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915467"
---
# <a name="driver-tasks"></a>드라이버 작업
드라이버에서 수행 하는 특정 작업은 다음과 같습니다.  
  
-   에 연결 하 고 데이터 원본에서 해제 합니다.  
  
-   드라이버 관리자에서 확인 하지 함수 오류를 검사 합니다.  
  
-   트랜잭션 시작 이 응용 프로그램에 투명 합니다.  
  
-   SQL 문 실행에 대 한 데이터 원본에 제출합니다. 드라이버는 ODBC SQL DBMS 관련 SQL;을 수정 해야 합니다. 이 방식은 비용 DBMS 관련 SQL 사용 하 여 ODBC에서 정의 된 이스케이프 절을 바꾸는 것을 제한 합니다.  
  
-   데이터를 전송 및 응용 프로그램에서 지정 된 대로 데이터 형식으로 변환 하는 포함 하 여 데이터 원본에서 데이터를 검색 합니다.  
  
-   DBMS 관련 오류를 ODBC Sqlstate에 매핑합니다.
