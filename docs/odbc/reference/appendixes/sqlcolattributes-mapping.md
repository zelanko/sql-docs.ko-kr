---
title: SQLColAttributes 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLColAttributes
- SQLColAttribute function [ODBC], mapping
ms.assetid: 30e25719-176b-4c48-97d4-920766b22412
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d0332e38a96d17589d9aa75bfe2a3c918dcc78d2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47639651"
---
# <a name="sqlcolattributes-mapping"></a>SQLColAttributes 매핑
응용 프로그램을 호출할 때 **SQLColAttributes** 는 ODBC 3 *.x* 드라이버, 호출 **SQLColAttributes** 매핑되 **SQLColAttribute** 다음과 같습니다.  
  
> [!NOTE]  
>  에 사용 되는 접두사 *FieldIdentifier* ODBC 3에서 값 *.x* 는에서 사용 되는 ODBC 2에서에서 변경 되었습니다. *x*합니다. 새 접두사는 "SQL_DESC"; 이전에는 "SQL_COLUMN" 했습니다.  
  
1.  응용 프로그램을 ODBC 2 인 경우 *x* 응용 프로그램 *fDescType* SQL_COLUMN_TYPE, 이며 반환 되는 형식은 간결한 DATETIME 형식으로 드라이버 관리자 맵에 date, time 및 timestamp 코드에 대 한 값을 반환 합니다.  
  
2.  경우 *fDescType* SQL_COLUMN_NAME, SQL_COLUMN_NULLABLE, 또는 SQL_COLUMN_COUNT, 드라이버 관리자 호출 **SQLColAttribute** 사용 하 여 드라이버에서를 *FieldIdentifier* 인수를 적절 하 게 SQL_DESC_NAME, SQL_DESC_NULLABLE, 또는 SQL_DESC_COUNT에 매핑된*합니다.* 다른 모든 값 *fDescType* 드라이버를 통해 전달 됩니다.  
  
 ODBC 3 *.x* 드라이버는 모든 ODBC 3을 지원 해야 *.x* *FieldIdentifiers* 에 대해 나열 된 **SQLColAttribute**합니다.  
  
 ODBC 3 *.x* SQL_COLUMN_PRECISION 및 자릿수가 SQL_DESC_PRECISION, SQL_COLUMN_SCALE 및 자릿수가 SQL_DESC_SCALE, 및 SQL_COLUMN_LENGTH 및 SQL_DESC_LENGTH 드라이버를 지원 해야 합니다. 전체 자릿수, 소수 자릿수 및 길이 ODBC 3에서 다르게 정의 되기 때문에 이러한 값은 다른 *.x* ODBC 2에 있는 것 보다. *x*합니다. 자세한 내용은 [열 크기, 십진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 d: 데이터 형식에서입니다.
