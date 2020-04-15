---
title: 확장 설정으로 새 데이터 형식 사용 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303414"
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>ExtendedAnsiSQL을 설정하여 새 데이터 형식을 사용하도록 설정
ExtendedAnsiSQL 플래그가 켜져 있을 때 Jet 4.0 데이터베이스에서 SQL_DECIMAL 및 SQL_NUMERIC 두 가지 새로운 데이터 형식을 사용할 수 있습니다. 기본 정밀도와 배율은 각각 18과 0입니다. SQL_DECIMAL 또는 SQL_NUMERIC 입력된 ODBC를 통해 액세스되는 데이터는 통화 대신 Microsoft Jet 소수점으로 매핑됩니다.  
  
 ExtendedAnsiSQL 플래그가 꺼져 있으면 소수점 또는 숫자 형식이 있는 테이블을 만들 수 없으며 이러한 형식은 SQLGetTypeInfo()에 나타나지 않습니다. 그러나 테이블에 새 데이터 형식이 포함된 경우 올바른 데이터 형식과 함께 사용할 수 있습니다.
