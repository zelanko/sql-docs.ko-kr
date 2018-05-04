---
title: SQLColAttributes 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLColAttributes
- SQLColAttribute function [ODBC], mapping
ms.assetid: 30e25719-176b-4c48-97d4-920766b22412
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 615ee316c8fe515ebbd3d983cd32e70bbcb8681e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlcolattributes-mapping"></a>SQLColAttributes 매핑
응용 프로그램 호출 하는 경우 **SQLColAttributes** ODBC 3 *.x* 드라이버에 대 한 호출 **SQLColAttributes** 에 매핑된 **SQLColAttribute** 다음과 같습니다.  
  
> [!NOTE]  
>  사용 되는 접두사 *FieldIdentifier* ODBC 3에서 값 *.x* 에 사용 되는 ODBC 2에서에서 변경 되었습니다. *x*합니다. 새 접두사는 "SQL_DESC"; 이전 접두사 "SQL_COLUMN" 했습니다.  
  
1.  응용 프로그램이 있는 경우는 ODBC 2. *x* 응용 프로그램을 *fDescType* SQL_COLUMN_TYPE, 이므로 반환 되는 형식은 간결한 DATETIME 형식으로 반환 되는 값을 date, time 및 timestamp 코드에 대 한 드라이버 관리자 맵.  
  
2.  경우 *fDescType* SQL_COLUMN_NAME, SQL_COLUMN_NULLABLE, 또는 SQL_COLUMN_COUNT, 드라이버 관리자를 호출 하 여 **SQLColAttribute** 사용 하 여 드라이버에는 *FieldIdentifier* 인수를 적절 하 게 SQL_DESC_NAME, SQL_DESC_NULLABLE, 또는 SQL_DESC_COUNT에 매핑된*합니다.* 다른 모든 값 *fDescType* 드라이버를 통해 전달 됩니다.  
  
 ODBC 3 *.x* 모든 ODBC 3을 지원 해야 *.x* *FieldIdentifiers* 에 대해 나열 된 **SQLColAttribute**합니다.  
  
 ODBC 3 *.x* SQL_COLUMN_PRECISION 및 SQL_DESC_PRECISION, SQL_COLUMN_SCALE SQL_DESC_SCALE, 및 SQL_COLUMN_LENGTH 및 SQL_DESC_LENGTH 드라이버 지원 해야 합니다. 전체 자릿수, 소수 자릿수 및 길이 ODBC 3에서는 다르게 정의 되기 때문에 이러한 값은 다른 *.x* 보다 ODBC 2. *x*합니다. 자세한 내용은 참조 [열 크기, 10 진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 d: 데이터 형식에서입니다.
