---
title: "트랜잭션 지원 Dbms에 | Microsoft Docs"
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
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 0fc2ae34-4748-4120-9fc3-bb28c8ed867e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 14c1519122484542b57e286c248c25c3fd6c0886
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="transaction-support-in-dbmss"></a>Dbms의 트랜잭션 지원
특히 데스크톱 데이터베이스 dBASE, Paradox 및 Btrieve, 같은 일부 데이터베이스에는 트랜잭션을 지원 하지 않습니다. 트랜잭션을 지 원하는 데이터베이스 간에 트랜잭션에서 않을 수 있는 SQL 문의 종류를 변형이 있습니다. 자세한 내용은 참조 SQL_TXN_CAPABLE 옵션에는 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명 합니다.
