---
title: SQLColAttributes 매핑 | 마이크로 소프트 문서
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
ms.openlocfilehash: 5c2c8386d6771141eaa0145a5d5964d70d6084d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305419"
---
# <a name="sqlcolattributes-mapping"></a>SQLColAttributes 매핑
응용 프로그램이 ODBC *3.x* 드라이버를 통해 **SQLColAttributes를** 호출하면 SQLColAttributes 호출은 다음과 같이 **SQLColAttribute에** **매핑됩니다.**  
  
> [!NOTE]
>  ODBC *3.x의* *FieldIdentifier* 값에 사용되는 접두사는 ODBC *2.x에서*사용되는 접두사와 변경되었습니다. 새 접두사는 "SQL_DESC"입니다. 이전 접두사는 "SQL_COLUMN"이었습니다.  
  
1.  응용 프로그램이 ODBC *2.x* 응용 프로그램인 경우 *fDescType이* SQL_COLUMN_TYPE 반환된 형식이 간결한 DATETIME 형식인 경우 드라이버 관리자는 날짜, 시간 및 타임스탬프 코드에 대한 반환 값을 매핑합니다.  
  
2.  *fDescType이* SQL_COLUMN_NAME, SQL_COLUMN_NULLABLE 또는 SQL_COLUMN_COUNT 경우 드라이버 관리자는 SQL_DESC_NAME, SQL_DESC_NULLABLE 또는 SQL_DESC_COUNT 매핑된 *FieldIdentifier* 인수를 사용하여 드라이버에서 **SQLColAttribute를** 호출합니다.*.* *fDescType의* 다른 모든 값은 드라이버에 전달됩니다.  
  
 ODBC *3.x* 드라이버는 **SQLColAttribute**에 대해 나열된 모든 ODBC *3.x* *필드식별자를* 지원해야 합니다.  
  
 ODBC *3.x* 드라이버는 SQL_COLUMN_PRECISION SQL_DESC_PRECISION, SQL_COLUMN_SCALE 및 SQL_DESC_SCALE, SQL_COLUMN_LENGTH 및 SQL_DESC_LENGTH 지원해야 합니다. 이러한 값은 ODBC *2.x에서와*다른 방식으로 ODBC *3.x에서* 정밀도, 배율 및 길이가 정의되기 때문에 다릅니다. 자세한 내용은 [열 크기, 소수 자릿수, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 유형의 표시 크기를 참조하십시오.
