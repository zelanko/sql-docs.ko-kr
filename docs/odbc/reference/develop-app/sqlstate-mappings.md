---
title: SQLSTATE 매핑 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3987085d7d04bf248bcc728c3bcd1ee5503d9af1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107358"
---
# <a name="sqlstate-mappings"></a>SQLSTATE 매핑(SQLSTATE Mappings)
이 항목 *에서는 odbc* *2.x 및 ODBC* 3.x의 SQLSTATE 값에 대해 설명 합니다. ODBC *3(sp3)* 의 SQLSTATE 값에 대 한 자세한 내용은 [부록 a: odbc 오류 코드](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)를 참조 하세요.  
  
 *ODBC 3.x에서는 S1xxx*대신 HYxxx sqlstates가 반환 되 고 S00XX 대신 42Sxx sqlstates가 반환 됩니다. 이 작업은 오픈 그룹 및 ISO 표준에 맞게 조정 되었습니다. 대부분의 경우 표준에서 여러 SQLSTATEs의 해석을 다시 정의 했으므로 매핑은 일대일가 아닙니다.  
  
 *Odbc 2.x* 응용 프로그램 *을 odbc 2.x 응용 프로그램* 으로 업그레이드할 *때 ODBC* 2.X sqlstates 대신 odbc *3.x sqlstates* 를 요구 하도록 응용 프로그램을 변경 해야 합니다. 다음 표에서는 각 ODBC *2.X SQLSTATE가 매핑되는 odbc* *3.x sqlstates* 를 나열 합니다.  
  
 SQL_ATTR_ODBC_VERSION 환경 특성을 SQL_OV_ODBC2로 설정 하면 **SQLGetDiagField** 또는 **SQLGetDiagRec** 가 호출 될 때 *드라이버가 ODBC* 2.X sqlstates 대신 odbc *2.x sqlstates* 를 게시 합니다. 특정 매핑은 열 2 *의 odbc 3.X* sqlstate에 해당 하는 다음 표의 열 1에서 확인 하 여 확인할 수 *있습니다.*  
  
|ODBC *2.X* SQLSTATE|ODBC *3(sp3)* SQLSTATE|주석|  
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
|S1001|HY001||  
|S1002|07009|원본 함수가 **SQLBindCol**, **sqlcolattribute**, **sqlcolattribute**, **Sqlfetch**, **Sqlcolattribute**또는 **SQLGetData**인 *경우 odbc 2.x* sqlstate S1002는 odbc *3.07009 x* 에 매핑됩니다.|  
|S1003|HY003||  
|S1004|HY004||  
|S1008|HY008||  
|S1009|HY009|Null 포인터를 잘못 사용 하는 경우 반환 됩니다.|  
|S1009|HY024|잘못 된 특성 값에 대해가 반환 되었습니다.|  
|S1009|HY092|동시성이 읽기 전용일 때 **SQLSetPos**를 호출 하 여 데이터를 업데이트 하거나 삭제 하거나 **SQLBulkOperations**호출을 통해 데이터를 추가, 업데이트 또는 삭제 하기 위해 반환 됩니다.|  
|S1010|HY007 HY010|SQLSTATE S1010는 **Sqlprepare**, **sqlexecdirect**또는 *StatementHandle*에 대 한 카탈로그 함수를 호출 하기 전에 **SQLDescribeCol** 가 호출 될 때 sqlstate HY007에 매핑됩니다. 그렇지 않은 경우 SQLSTATE S1010는 SQLSTATE HY010에 매핑됩니다.|  
|S1011|HY011||  
|S1012|HY012||  
|S1090|HY090||  
|S1091|HY091||  
|S1092|HY092||  
|S1093|07009|ODBC *3.X sqlstate 07009* 은 원본 함수가 **SQLBindParameter** 또는 **SQLDescribeParam**경우 odbc 2.x *sqlstate S1093에 매핑됩니다.*|  
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
|S1111|HY111||  
|S1C00|HYC00||  
|S1T00|HYT00||  
  
> [!NOTE]  
>  ODBC *3.X sqlstate 07008은 odbc 2.X* *sqlstate S1000* 에 매핑됩니다.
