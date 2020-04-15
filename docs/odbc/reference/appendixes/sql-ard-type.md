---
title: SQL_ARD_TYPE | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], SQL_ARD_TYPE
- SQL_ARD_TYPE [ODBC]
ms.assetid: 8d87ca10-f955-4284-8689-e9f4cc31e7ae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d7e28d6babb7db8364697ae62092256396b44914
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305034"
---
# <a name="sql_ard_type"></a>SQL_ARD_TYPE
SQL_ARD_TYPE 형식 식별자는 버퍼의 데이터가 ARD의 SQL_DESC_CONCISE_TYPE 필드에 지정된 형식임을 나타내는 데 사용됩니다. SQL_ARD_TYPE 특정 데이터 형식 대신 **SQLGetData** 호출의 *TargetType* 인수에 입력 되며 설명자 필드를 변경 하 여 버퍼의 데이터 형식을 변경할 수 있습니다. 이 값은 * \*TargetValuePtr* 버퍼의 데이터 형식을 설명자 필드에 연결합니다. 바인딩된 버퍼의 형식이 이미 SQL_DESC_TYPE 및 SQL_DESC_CONCISE_TYPE 필드에 연결되어 있고 해당 필드 중 하나를 변경하여 언제든지 변경할 수 있으므로 **SQL_ARD_TYPE SQLBindCol** 또는 **SQLBindParameter** 호출에 입력되지 않습니다.  
  
 SQL_ARD_TYPE 형식 식별자를 사용하여 간격 데이터 형식의 선행 정밀도 및 초 정밀도 및 SQL_C_NUMERIC 데이터 형식에 대한 정밀도 및 배율 값을 지정할 수 있습니다. 자세한 내용은 [간격 데이터 유형에 대한 기본 선행 및 초 정밀도 재정을 재사용하고](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md) 숫자 데이터 [형식에 대한 기본 정밀도 및 배율 재정의를](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md)참조하세요.
