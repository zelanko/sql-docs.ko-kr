---
title: SQLGetDiagRec 및 SQLGetDiagField 구현 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a4b602d5ff4a94d2888395e6a62f03553fb50f98
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68216369"
---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>SQLGetDiagRec 및 SQLGetDiagField 구현
**SQLGetDiagRec** 하 고 **SQLGetDiagField** 드라이버 관리자와 각 드라이버에 의해 구현 됩니다. 드라이버 관리자 및 각 드라이버 각 환경, 연결, 문 및 설명자 핸들에 대 한 진단 레코드를 유지 하 고 핸들 또는 핸들 해제가 사용 하 여 다른 함수를 호출할 경우에 이러한 레코드를 해제 합니다.  
  
 드라이버 관리자와 각 드라이버의 순위에 따라 첫 번째 상태 레코드를 확인 해야 하지만 [상태 레코드의 시퀀스](../../../odbc/reference/develop-app/sequence-of-status-records.md), 드라이버 관리자는 최종 레코드 시퀀스를 결정 합니다.  
  
 **SQLGetDiagRec** 하 고 **SQLGetDiagField** 자신에 대 한 진단 레코드를 게시 하지 마십시오.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [진단 처리 규칙](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [드라이버 관리자의 역할](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [드라이버의 역할](../../../odbc/reference/develop-app/role-of-the-driver.md)
