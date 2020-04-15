---
title: SQL_NO_DATA | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
ms.assetid: deed0163-9d1a-4e9b-9342-3f82e64477d2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e2c806edd5d5647e09c00975ad7207ee5c2c876
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305114"
---
# <a name="returning-sql_no_data"></a>SQL_NO_DATA 반환
ODBC *3.x* 드라이버로 작업하는 ODBC *2.x* 응용 프로그램이 **SQLExecDirect,** **SQLExecute**또는 **SQLParamData를**호출하고 검색된 업데이트 또는 삭제 문이 실행되었지만 데이터 원본의 행에 영향을 주지 않는 경우 ODBC *3.x* 드라이버는 SQL_SUCCESS 반환해야 합니다. ODBC *3.x* 드라이버로 작업하는 ODBC *3.x* 응용 프로그램이 **SQLExecDirect,** **SQLExecute**또는 **SQLParamData를** 호출하는 경우 와 같은 결과를 가진 경우 ODBC *3.x* 드라이버는 SQL_NO_DATA 반환해야 합니다.  
  
 문 일괄 처리에서 검색된 업데이트 또는 delete 문이 데이터 원본의 행에 영향을 주지 않는 경우 **SQLMoreResults는** SQL_SUCCESS 반환합니다. SQL_NO_DATA 반환할 수 없습니다.
