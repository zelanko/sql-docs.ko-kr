---
description: SQLGetDiagRec 및 SQLGetDiagField 구현
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 91e43252aea4ebf12dedcb14bb1b7fb34f75df6f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461435"
---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>SQLGetDiagRec 및 SQLGetDiagField 구현
**SQLGetDiagRec** 및 **SQLGetDiagField** 는 드라이버 관리자 및 각 드라이버에 의해 구현 됩니다. 드라이버 관리자와 각 드라이버는 각 환경, 연결, 문 및 설명자 핸들에 대 한 진단 레코드를 유지 관리 하 고 해당 핸들을 사용 하 여 다른 함수를 호출 하거나 핸들이 해제 된 경우에만 해당 레코드를 해제 합니다.  
  
 드라이버 관리자와 각 드라이버는 [상태 레코드 시퀀스](../../../odbc/reference/develop-app/sequence-of-status-records.md)의 순위에 따라 첫 번째 상태 레코드를 결정 해야 하지만, 드라이버 관리자는 마지막 레코드 시퀀스를 결정 합니다.  
  
 **SQLGetDiagRec** 및 **SQLGetDiagField** 는 자체에 대 한 진단 레코드를 게시 하지 않습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [진단 처리 규칙](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [드라이버 관리자의 역할](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [드라이버의 역할](../../../odbc/reference/develop-app/role-of-the-driver.md)
