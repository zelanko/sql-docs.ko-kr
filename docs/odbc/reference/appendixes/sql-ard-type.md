---
title: SQL_ARD_TYPE | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305034"
---
# <a name="sql_ard_type"></a>SQL_ARD_TYPE
SQL_ARD_TYPE 형식 식별자는 버퍼의 데이터가 사용 하는 SQL_DESC_CONCISE_TYPE 필드에 지정 된 형식이 되도록 나타내는 데 사용 됩니다. SQL_ARD_TYPE는 특정 데이터 형식이 아닌 **SQLGetData** 호출의 *TargetType* 인수에 입력 되며 응용 프로그램에서 설명자 필드를 변경 하 여 버퍼의 데이터 형식을 변경할 수 있도록 합니다. 이 값은 * \*targetvalueptr* 버퍼의 데이터 형식을 설명자 필드에 연결 합니다. **SQLBindCol** 또는 **SQLBindParameter** 에 대 한 호출에는 바인딩된 버퍼의 형식이 이미 SQL_DESC_TYPE 및 SQL_DESC_CONCISE_TYPE 필드에 연결 되어 있으며, 이러한 필드 중 하나를 변경 하 여 언제 든 지 변경할 수 있으므로 SQL_ARD_TYPE는 호출에 입력 되지 않습니다.  
  
 SQL_ARD_TYPE 형식 식별자를 사용 하 여 간격 데이터 형식의 선행 전체 자릿수와 초 정밀도에 대해 기본값이 아닌 값을 지정 하 고 SQL_C_NUMERIC 데이터 형식에 대 한 전체 자릿수 및 소수 자릿수 값을 지정할 수 있습니다. 자세한 내용은이 부록 뒷부분의 [Interval 데이터 형식에 대 한 기본 선행 및 초 전체 자릿수 재정의](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md) 및 [숫자 데이터 형식에 대 한 기본 전체 자릿수 및 소수 자릿수 재정의](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md)를 참조 하세요.
