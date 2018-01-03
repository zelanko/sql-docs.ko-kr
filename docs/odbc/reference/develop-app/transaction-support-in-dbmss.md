---
title: "트랜잭션 지원 Dbms에 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 0fc2ae34-4748-4120-9fc3-bb28c8ed867e
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9b20cef18c97b0195bb42b687394bf3756a5f225
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="transaction-support-in-dbmss"></a>Dbms의 트랜잭션 지원
특히 데스크톱 데이터베이스 dBASE, Paradox 및 Btrieve, 같은 일부 데이터베이스에는 트랜잭션을 지원 하지 않습니다. 트랜잭션을 지 원하는 데이터베이스 간에 트랜잭션에서 않을 수 있는 SQL 문의 종류를 변형이 있습니다. 자세한 내용은 참조 SQL_TXN_CAPABLE 옵션에는 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명 합니다.
