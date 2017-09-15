---
title: "SQLGetDiagRec 및 SQLGetDiagField 구현 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 11ba1857-b533-4517-8131-a2a8a0154a0a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 463ddfe552c94a9e90ceb2a24f8061674955979d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>SQLGetDiagRec 및 SQLGetDiagField 구현
**SQLGetDiagRec** 및 **SQLGetDiagField** 드라이버 관리자와 각 드라이버에 의해 구현 됩니다. 드라이버 관리자 및 각 드라이버에는 각 환경, 연결, 문 및 설명자 핸들에 대 한 진단 레코드를 유지 하 고 사용 핸들 또는 핸들이 해제 될 하는 다른 함수를 호출 하는 경우에 이러한 레코드를 비울 합니다.  
  
 드라이버 관리자와 각 드라이버에 대 한 순위에 따라 첫 번째 상태 레코드를 결정 해야 하지만 [상태 레코드의 시퀀스](../../../odbc/reference/develop-app/sequence-of-status-records.md), 드라이버 관리자 레코드의 마지막 시퀀스를 결정 합니다.  
  
 **SQLGetDiagRec** 및 **SQLGetDiagField** 자신에 대 한 진단 레코드를 게시 하지 마십시오.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [진단 처리 규칙](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [드라이버 관리자의 역할](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [드라이버의 역할](../../../odbc/reference/develop-app/role-of-the-driver.md)
