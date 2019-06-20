---
title: Extendedansisql을 설정 하 여 새 데이터 형식을 사용 하도록 설정 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 80a86ef188796883e76c6d5f6149a3e40afd341b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63128003"
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>ExtendedAnsiSQL을 설정하여 새 데이터 형식을 사용하도록 설정
Extendedansisql을 플래그를 켤 때 두 개의 새 데이터 형식을 Jet 4.0 데이터베이스에서 사용할 수 있습니다. SQL_DECIMAL 및 SQL_NUMERIC 합니다. 기본 전체 자릿수 및 확장은 각각 18과 0입니다. SQL_DECIMAL 또는 SQL_NUMERIC로 형식화 된 ODBC를 통해 액세스 되는 데이터는 통화 하는 대신 Microsoft Jet Decimal에 매핑됩니다.  
  
 Extendedansisql을 플래그를 해제 하 고, 소수 또는 숫자 형식으로 테이블을 만들 수 없습니다 및 이러한 형식을 SQLGetTypeInfo()에 나타나지 않습니다. 그러나 테이블에 새 데이터 형식이 들어 하는 경우 올바른 데이터 형식에 사용할 수 있습니다.
