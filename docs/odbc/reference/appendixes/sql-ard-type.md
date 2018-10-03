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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 683b81f82094aa33deef86ffc19dc8c5c0a53a27
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47669851"
---
# <a name="sqlardtype"></a>SQL_ARD_TYPE
SQL_ARD_TYPE 형식 식별자는 버퍼의 데이터는 카드가 SQL_DESC_CONCISE_TYPE 필드에 지정 된 형식의 될 것임을 나타내려면 됩니다. SQL_ARD_TYPE에 입력 합니다 *TargetType* 에 대 한 호출의 인수 **SQLGetData** 특정 데이터 형식 및 데이터를 변경 하는 응용 프로그램 설명자를 변경 하 여 버퍼의 입력을 사용 하도록 설정 하는 대신 필드입니다. 이 값의 데이터 형식을 연결 합니다  *\*TargetValuePtr* 버퍼 설명자 필드입니다. (SQL_ARD_TYPE에 대 한 호출에 입력 되지 않았습니다 **SQLBindCol** 하거나 **SQLBindParameter** 바인딩된 버퍼 유형의 SQL_DESC_TYPE 및 SQL_DESC_CONCISE_TYPE 필드를 이미 연결 되어 있고 변경할 수 있습니다 때문에 언제 든 지 이러한 필드 중 하나를 변경 합니다.)  
  
 선행 정밀도 및 interval 데이터 형식의 초 전체 자릿수에 대 한 기본이 아닌 값을 지정 하려면 SQL_ARD_TYPE 형식 식별자를 사용할 수 있습니다 및 SQL_C_NUMERIC 데이터에 대 한 전체 자릿수 및 소수 자릿수 값을 입력 합니다. 자세한 내용은 [재정의 기본 선행 및 초 간격 데이터 형식 전체 자릿수](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md) 하 고 [재정의 기본 전체 자릿수 및 소수 자릿수 숫자 데이터 형식입니다](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md)이 부록의 뒷부분에 나오는.
