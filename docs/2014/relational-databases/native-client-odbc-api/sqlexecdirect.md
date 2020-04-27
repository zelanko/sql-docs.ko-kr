---
title: SQLExecDirect | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLExecDirect function
ms.assetid: e7c2a5b5-83f4-4c72-9aca-7b9fb4748b11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f9e4790cfae631a9a977431f25282aae766f3e3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63067514"
---
# <a name="sqlexecdirect"></a>SQLExecDirect
  SQL_SOPT_SS_PARAM_FOCUS statement 특성이 0이 아니면 SQLExecDirect는 SQL_ERROR를 반환 하 고 SQLSTATE = HY024 및 "잘못 된 특성 값 SQL_SOPT_SS_PARAM_FOCUS (실행 시 0 이어야 함)" 라는 메시지가 포함 된 진단 레코드를 생성 합니다. SQL_SOPT_SS_PARAM_FOCUS에 대한 자세한 내용은 [SQLSetStmtAttr](sqlsetstmtattr.md)을 참조하십시오.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 [ODBC&#41;&#40;테이블 반환 매개 변수 ](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=80709)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
