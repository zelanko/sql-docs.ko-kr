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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1b30df63a3c955d2ed074ab13649ea55c21a6da7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81294203"
---
# <a name="driver-tasks"></a>드라이버 작업
드라이버에서 수행 되는 특정 작업은 다음과 같습니다.  
  
-   데이터 원본에 연결 하 고 데이터 원본에서 연결을 끊는 중입니다.  
  
-   드라이버 관리자에서 검사 하지 않은 함수 오류를 확인 하는 중입니다.  
  
-   트랜잭션 시작 이는 응용 프로그램에 투명 합니다.  
  
-   실행을 위해 데이터 원본에 SQL 문을 전송 합니다. 드라이버에서 ODBC SQL을 DBMS 관련 SQL로 수정 해야 합니다. 일반적으로 ODBC에 정의 된 이스케이프 절을 DBMS 관련 SQL로 대체 하는 것으로 제한 됩니다.  
  
-   응용 프로그램에 지정 된 데이터 형식 변환을 포함 하 여 데이터 소스에서 데이터를 보내고 검색 합니다.  
  
-   DBMS 관련 오류를 ODBC SQLSTATEs에 매핑합니다.
