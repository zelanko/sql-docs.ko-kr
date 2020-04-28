---
title: Extendedansisql을를 설정 하 여 새 데이터 형식 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], enabling new data types
ms.assetid: f2865543-7fff-44fa-9a6a-968bec33acdc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b703c5c14c4743e13feee139d16e5dfeb3c24c63
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303414"
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>ExtendedAnsiSQL을 설정하여 새 데이터 형식을 사용하도록 설정
Extendedansisql을 플래그가 설정 되 면 Jet 4.0 데이터베이스에서 두 가지 새 데이터 형식 (SQL_DECIMAL 및 SQL_NUMERIC을 사용할 수 있습니다. 기본 전체 자릿수와 소수 자릿수는 각각 18과 0입니다. SQL_DECIMAL 또는 SQL_NUMERIC 형식화 된 ODBC를 통해 액세스 되는 데이터는 통화 대신 Microsoft Jet 10 진수에 매핑됩니다.  
  
 Extendedansisql을 플래그가 꺼져 있으면 decimal 또는 numeric 형식의 테이블을 만들 수 없으며 이러한 형식은 SQLGetTypeInfo ()에 표시 되지 않습니다. 그러나 테이블에 새 데이터 형식이 포함 된 경우에는 올바른 데이터 형식으로 사용할 수 있습니다.
