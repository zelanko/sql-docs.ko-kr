---
description: SQLColAttributes 매핑
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 864f81877e548de9bbb0478e9313c2cd38dd3838
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466045"
---
# <a name="sqlcolattributes-mapping"></a>SQLColAttributes 매핑
응용 *프로그램이 ODBC 3.x* 드라이버를 통해 **sqlcolattributes** 를 호출 하는 경우 **sqlcolattributes** 에 대 한 호출은 다음과 같이 **sqlcolattributes** 에 매핑됩니다.  
  
> [!NOTE]
>  *Odbc 3.x* 의 *FieldIdentifier* 값에 사용 된 접두사는 odbc 2.x에서 사용 된 접두사에서 변경 되었습니다 *.* 새 접두사는 "SQL_DESC"입니다. 이전 접두사는 "SQL_COLUMN"입니다.  
  
1.  응용 *프로그램이 ODBC 2.x* 응용 프로그램이 고 반환 된 형식이 간결한 날짜/시간 형식인 경우 드라이버 관리자는 날짜, 시간 및 타임 스탬프 코드에 대 한 반환 값을 SQL_COLUMN_TYPE *fDescType* 합니다.  
  
2.  *FDescType* 가 SQL_COLUMN_NAME, SQL_COLUMN_NULLABLE 또는 SQL_COLUMN_COUNT 경우 드라이버 관리자는 적절 하 게 SQL_DESC_NAME, SQL_DESC_NULLABLE 또는 SQL_DESC_COUNT에 매핑된 *FieldIdentifier* 인수를 사용 하 여 드라이버에서 **sqlcolattribute** 를 호출 합니다 *.* *FDescType* 의 다른 모든 값은 드라이버에 전달 됩니다.  
  
 ODBC 3.x *드라이버는* **sqlcolattribute**에 대해 나열 된 모든 odbc *3(sp3)* *FieldIdentifiers* 을 지원 해야 합니다.  
  
 ODBC 3.x 드라이버는 SQL_COLUMN_PRECISION 및 SQL_DESC_PRECISION, SQL_COLUMN_SCALE 및 SQL_DESC_SCALE, SQL_COLUMN_LENGTH 및 SQL_DESC_LENGTH를 지원 해야 *합니다.* 이러한 값은 전체 자릿수, 소수 자릿수 및 *길이가 odbc 2.x*와는 *달리 odbc 2.x* 에서 다르게 정의 되기 때문에 다릅니다. 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 형식의 표시 크기를 참조 하세요.
