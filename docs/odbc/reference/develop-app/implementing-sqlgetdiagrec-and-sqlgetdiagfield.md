---
title: SQLGetDiagRec 및 SQLGetDiagField 구현 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 11ba1857-b533-4517-8131-a2a8a0154a0a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4c090af19a9296e46e3036ca23f6c97298bcb1b8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300143"
---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>SQLGetDiagRec 및 SQLGetDiagField 구현
**SQLGetDiagRec** 및 **SQLGetDiagField는** 드라이버 관리자와 각 드라이버에 의해 구현됩니다. 드라이버 관리자와 각 드라이버는 각 환경, 연결, 명령문 및 설명자 핸들에 대한 진단 레코드를 유지 관리하며 해당 핸들을 사용 해 다른 함수가 호출되거나 핸들이 해제될 때만 해당 레코드를 해제합니다.  
  
 드라이버 관리자와 각 드라이버 모두 [상태 레코드 시퀀스의](../../../odbc/reference/develop-app/sequence-of-status-records.md)순위에 따라 첫 번째 상태 레코드를 결정해야 하지만 드라이버 관리자는 레코드의 최종 시퀀스를 결정합니다.  
  
 **SQLGetDiagRec** 및 **SQLGetDiagField는** 자신에 대한 진단 기록을 게시하지 않습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [진단 처리 규칙](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [드라이버 관리자의 역할](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [드라이버의 역할](../../../odbc/reference/develop-app/role-of-the-driver.md)
