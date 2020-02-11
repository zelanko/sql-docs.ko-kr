---
title: Dbms의 트랜잭션 지원 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 0fc2ae34-4748-4120-9fc3-bb28c8ed867e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 72353e9917996ecacdc5971b4a11f9c73718ba43
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037636"
---
# <a name="transaction-support-in-dbmss"></a>DBMS의 트랜잭션 지원
일부 데이터베이스, 특히 dBASE, Paradox, Btrieve 등의 데스크톱 데이터베이스는 트랜잭션을 지원 하지 않습니다. 트랜잭션을 지 원하는 데이터베이스 간에도 트랜잭션에 있을 수 있는 SQL 문의 종류에는 변형이 있습니다. 자세한 내용은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명의 SQL_TXN_CAPABLE 옵션을 참조 하십시오.
