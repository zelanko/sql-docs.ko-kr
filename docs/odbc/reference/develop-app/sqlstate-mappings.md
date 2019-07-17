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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107358"
---
# <a name="sqlstate-mappings"></a>SQLSTATE 매핑(SQLSTATE Mappings)
이 항목에서는 odbc SQLSTATE 값 설명 *2.x* 및 ODBC *3.x*합니다. ODBC에 대 한 자세한 내용은 *3.x* SQLSTATE 값 참조 [부록 a: ODBC 오류 코드](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)합니다.  
  
 Odbc에서 *3.x*HYxxx SQLSTATEs S1xxx를 대신 반환 되 고 42Sxx SQLSTATEs S00XX 대신 반환 됩니다. 이 작업은 Open Group 및 ISO 표준에 맞게 수행 되었습니다. 대부분의 경우에서 매핑을 아니므로 일대일 표준을 여러 SQLSTATEs의 해석은 다시 정의 했습니다.  
  
 때 ODBC *2.x* 는 odbc 응용 프로그램을 업그레이드할 *3.x* ODBC 예상 변경 수 응용 프로그램, 응용 프로그램에 *3.x* ODBC 대신Sqlstate*2.x* Sqlstate입니다. 다음 표에서 ODBC *3.x* Sqlstate는 각 ODBC *2.x* SQLSTATE 매핑됩니다.  
  
 ODBC 드라이버에 게시물 SQL_OV_ODBC2를 SQL_ATTR_ODBC_VERSION 환경 특성을 설정 하면 *2.x* 대신 ODBC Sqlstate *3.x* SQLSTATEs 때 **SQLGetDiagField**나 **SQLGetDiagRec** 라고 합니다. ODBC를 살펴보면 특정 매핑을 확인할 수 있습니다 *2.x* ODBC에 해당 하는 다음 테이블의 열 1에서에서 SQLSTATE *3.x* 열 2의에서 SQLSTATE입니다.  
  
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
|S1001|HY001||  
|S1002|07009|ODBC *2.x* ODBC SQLSTATE S1002 매핑됩니다 *3.x* 07009 기본 함수는 경우 SQLSTATE **SQLBindCol**를 **SQLColAttribute**, **SQLExtendedFetch**, **SQLFetch**하십시오 **SQLFetchScroll**, 또는 **SQLGetData**합니다.|  
|S1003|HY003||  
|S1004|HY004||  
|S1008|HY008||  
|S1009|HY009|Null 포인터를 잘못 사용에 대 한 반환 합니다.|  
|S1009|HY024|잘못 된 특성 값에 대해 반환 됩니다.|  
|S1009|HY092|호출 하 여 데이터를 삭제 또는 업데이트에 대 한 반환 **SQLSetPos**, 또는 추가, 업데이트 또는를 호출 하 여 데이터를 삭제 **SQLBulkOperations**동시성 읽기 전용인 경우.|  
|S1010|HY007 HY010|SQLSTATE S1010 SQLSTATE HY007 매핑되는 경우 **SQLDescribeCol** 호출 하기 전에 호출 됩니다 **SQLPrepare**, **SQLExecDirect**, 또는 카탈로그 함수에는 *StatementHandle*합니다. 그렇지 않으면 SQLSTATE S1010 SQLSTATE HY010에 매핑됩니다.|  
|S1011|HY011||  
|S1012|HY012||  
|S1090|HY090||  
|S1091|HY091||  
|S1092|HY092||  
|S1093|07009|ODBC *3.x* ODBC SQLSTATE 07009 매핑됩니다 *2.x* SQLSTATE S1093 기본 함수가 **SQLBindParameter** 또는 **SQLDescribeParam**.|  
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
>  ODBC *3.x* ODBC SQLSTATE 07008 매핑됩니다 *2.x* SQLSTATE S1000 합니다.
