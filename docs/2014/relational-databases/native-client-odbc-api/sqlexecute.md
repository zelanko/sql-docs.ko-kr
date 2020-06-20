---
title: SQLExecute | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLExecute function
ms.assetid: 4d7db8b6-611f-4fe4-be85-2a407059de45
author: rothja
ms.author: jroth
ms.openlocfilehash: 514436c65ef103cafae2189a03b560255b447eda
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85022527"
---
# <a name="sqlexecute"></a>SQLExecute
  SQL_SOPT_SS_PARAM_FOCUS statement 특성이 0으로 설정 되지 않은 경우 SQLExecute는 SQL_ERROR를 반환 하 고 SQLSTATE = HY024 및 "잘못 된 특성 값, SQL_SOPT_SS_PARAM_FOCUS (실행 시 0 이어야 함)" 라는 메시지와 함께 진단 레코드를 생성 합니다. SQL_SOPT_SS_PARAM_FOCUS에 대한 자세한 내용은 [SQLSetStmtAttr](sqlsetstmtattr.md)을 참조하십시오.  
  
## <a name="remarks"></a>설명  
 테이블 반환 매개 변수에 대 한 자세한 내용은 [ODBC&#41;&#40;테이블 반환 매개 변수 ](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLExecute](https://go.microsoft.com/fwlink/?LinkId=80708)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
