---
title: SQLSTATE 매핑 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSTATE
- backward compatibility [ODBC], SQLSTATE
- SQLSTATE [ODBC]
ms.assetid: 6e6cabcf-a204-40eb-b77d-8a0c4a5e8524
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec58c0e41869529bbba5fd31ad534976923a990d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299743"
---
# <a name="sqlstate-mappings"></a>SQLSTATE 매핑(SQLSTATE Mappings)
이 항목에서는 ODBC *2.x* 및 ODBC *3.x에*대한 SQLSTATE 값에 대해 설명합니다. ODBC *3.x* SQLSTATE 값에 대한 자세한 내용은 [부록 A: ODBC 오류 코드](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)를 참조하십시오.  
  
 ODBC *3.x에서*HYxxx SQLSTATEs는 S1xxx 대신 반환되고 42Sxx SQLSTAT는 S00XX 대신 반환됩니다. 이것은 오픈 그룹 및 ISO 표준에 부합하기 위해 수행되었습니다. 대부분의 경우 표준이 여러 SQLSTAT의 해석을 재정의했기 때문에 매핑이 일대일이 아닙니다.  
  
 ODBC *2.x* 응용 프로그램이 ODBC *3.x* 응용 프로그램으로 업그레이드되는 경우 응용 프로그램을 ODBC *2.x* SQLSTATEs 대신 ODBC *3.x* SQLSTATE를 예상하도록 변경해야 합니다. 다음 표에는 각 ODBC *2.x* SQLSTATE가 매핑되는 ODBC *3.x* SQLSTATEs가 나열되어 있습니다.  
  
 SQL_ATTR_ODBC_VERSION 환경 특성이 SQL_OV_ODBC2 설정되면 **SQLGetDiagField** 또는 **SQLGetDiagRec이** 호출될 때 드라이버는 ODBC *3.x* SQLSTATEs 대신 ODBC *2.x* SQLSTATEs를 게시합니다. 특정 매핑은 열 2의 ODBC *3.x* SQLSTATE에 해당하는 다음 표의 열 1에 있는 ODBC *2.x* SQLSTATE를 지니서 결정할 수 있습니다.  
  
|ODBC *2.x* SQLSTATE|ODBC *3.x* SQLSTATE|주석|  
|-------------------------|-------------------------|--------------|  
|01S03|01001||  
|01S04|01001||  
|22003|HY019||  
|22008|22007||  
|22005|22018||  
|24000|07005||  
|37000|42000||  
|70100|HY018||  
|S0001|42S01||  
|S0002|42S02||  
|S0011|42S11||  
|S0012|42S12||  
|S0021|42S21||  
|S0022|42S22||  
|S0023|42S23||  
|S1000|HY000||  
|S1001|HY01||  
|S1002|07009|ODBC *2.x* SQLSTATE S1002는 기본 함수가 **SQLBindCol,** **SQLColAttribute**, **SQLExtendedFetch**, **SQLFetch**, **SQLFetch스크롤,** **SQLGetData 또는 SQLGetData**인 경우 ODBC *3.x* SQLSTATE 07009에 매핑됩니다.|  
|S1003|HY003||  
|S1004|HY004||  
|S1008|HY08||  
|S1009|HY09|null 포인터를 잘못 사용하여 반환되었습니다.|  
|S1009|HY024|잘못된 특성 값에 대해 반환되었습니다.|  
|S1009|HY092|동시성을 읽을 때 **SQLSetPos를**호출하여 데이터를 업데이트하거나 삭제하거나 **SQLBulkOperations를**호출하여 데이터를 추가, 업데이트 또는 삭제하는 데 반환됩니다.|  
|S1010|HY007 HY010|SQLSTATE S1010은 SQLState HY007에 매핑됩니다 **SQLDescribeCol** **SQLPrepare,** **SQLExecDirect**또는 *문 핸들에*대 한 카탈로그 함수를 호출 하기 전에 호출 됩니다. 그렇지 않으면 SQLSTATE S1010이 SQLSTATE HY010에 매핑됩니다.|  
|S1011|HY011||  
|S1012|HY012||  
|S1090|HY090||  
|S1091|HY091||  
|S1092|HY092||  
|S1093|07009|ODBC *3.x* SQLSTATE 07009는 기본 함수가 **SQLBindParameter** 또는 **SQLDescribeParam인**경우 ODBC *2.x* SQLSTATE S1093에 매핑됩니다.|  
|S1096|HY096||  
|S1097|HY097||  
|S1098|HY098||  
|S1099|HY099||  
|S1100|HY100||  
|S1101|HY101||  
|S1103|HY103||  
|S1104|HY104||  
|S1105|HY105||  
|S1106|HY106||  
|S1107|HY107||  
|S1108|HY108||  
|S1109|HY109||  
|S1110|HY110||  
|S1111|HY11||  
|S1C00|하이크00||  
|S1T00|HYT00||  
  
> [!NOTE]  
>  ODBC *3.x* SQLSTATE 07008은 ODBC *2.x* SQLSTATE S1000에 매핑됩니다.
