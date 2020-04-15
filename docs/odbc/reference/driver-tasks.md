---
title: 드라이버 작업 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294203"
---
# <a name="driver-tasks"></a>드라이버 작업
드라이버가 수행하는 특정 작업은 다음과 같습니다.  
  
-   데이터 원본에 연결하고 연결을 끊습니다.  
  
-   드라이버 관리자에서 확인하지 않은 함수 오류를 검사합니다.  
  
-   트랜잭션 을 다시 이는 응용 프로그램에 투명합니다.  
  
-   실행을 위해 데이터 원본에 SQL 문을 제출합니다. 드라이버는 ODBC SQL을 DBMS 별 SQL로 수정해야 합니다. 이는 ODBC에서 정의한 이스케이프 절을 DBMS 별 SQL로 대체하는 것으로 제한되는 경우가 많습니다.  
  
-   응용 프로그램에서 지정한 데이터 형식을 변환하는 것을 포함하여 데이터 원본으로 데이터를 보내고 데이터를 검색합니다.  
  
-   DBMS 관련 오류를 ODBC SQLSTATEs에 매핑합니다.
