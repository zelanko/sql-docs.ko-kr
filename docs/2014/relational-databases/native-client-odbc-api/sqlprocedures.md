---
title: SQLProcedures Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0001f1d6e45e855b884028a595a2b61263c2e58
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63046689"
---
# <a name="sqlprocedures"></a>SQLProcedures
  모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저는 값을 반환합니다. **Sqlprocedures** 는 결과 집합 열 PROCEDURE_TYPE에 대 한 SQL_PT_FUNCTION를 보고 합니다.  
  
 **Sqlprocedures** *CatalogName, SchemaName* 또는 *ProcName* 매개 변수에 대 한 값이 있는지 여부를 SQL_SUCCESS을 반환 합니다. 이러한 매개 변수에 잘못 된 값이 사용 되는 경우 **Sqlfetch** SQL_NO_DATA 반환 합니다.  
  
 **Sqlprocedures** 는 정적 서버 커서에 대해 실행할 수 있습니다. 업데이트할 수 있는 (동적 또는 키 집합) 커서에 대해 **Sqlprocedures** 를 실행 하려고 하면 커서 유형이 변경 되었음을 나타내는 SQL_SUCCESS_WITH_INFO 반환 됩니다.  
  
 **Sqlprocedures** 는 이름이 *ProcName* 와 일치 하 고 현재 사용자가 실행 하거나 현재 사용자에 게 VIEW DEFINITION 권한이 부여 된 프로시저에 대 한 정보를 반환 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLProcedures 함수](https://go.microsoft.com/fwlink/?LinkId=59364)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
