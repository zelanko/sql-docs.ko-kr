---
title: ExtendedAnsiSQL를 설정 하 여 새 데이터 형식을 활성화 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- extendedANSISQL [ODBC], enabling new data types
ms.assetid: f2865543-7fff-44fa-9a6a-968bec33acdc
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4909c520ab4398123bab9159ecd26a538c3bbd52
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>ExtendedAnsiSQL를 설정 하 여 새 데이터 형식을 사용 하도록 설정
ExtendedAnsiSQL 플래그 상태에서 두 개의 새 데이터 형식을 Jet 4.0 데이터베이스에서 사용할 수는: SQL_DECIMAL 및 SQL_NUMERIC 합니다. 기본 전체 자릿수 및 소수 자릿수는 18과 0 각각입니다. SQL_DECIMAL 또는 SQL_NUMERIC로 형식화 된 ODBC를 통해 액세스 되는 데이터는 통화 하는 대신 Microsoft Jet Decimal에 매핑됩니다.  
  
 ExtendedAnsiSQL 플래그를 해제 하 고, 10 진수 또는 숫자 형식으로 테이블을 만들 수 없습니다 및 이러한 형식을 SQLGetTypeInfo()에 표시 되지 않습니다. 그러나 테이블에 새 데이터 형식이 있으면 올바른 데이터 형식으로 사용 될 수 있습니다.
