---
description: DBMS의 트랜잭션 지원
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8e0b3433e0f666af100cce5e72e36b685533b1d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487456"
---
# <a name="transaction-support-in-dbmss"></a>DBMS의 트랜잭션 지원
일부 데이터베이스, 특히 dBASE, Paradox, Btrieve 등의 데스크톱 데이터베이스는 트랜잭션을 지원 하지 않습니다. 트랜잭션을 지 원하는 데이터베이스 간에도 트랜잭션에 있을 수 있는 SQL 문의 종류에는 변형이 있습니다. 자세한 내용은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명의 SQL_TXN_CAPABLE 옵션을 참조 하십시오.
