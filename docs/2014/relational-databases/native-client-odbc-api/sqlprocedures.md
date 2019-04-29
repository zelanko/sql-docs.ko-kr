---
title: SQLProcedures | Microsoft Docs
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
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63046689"
---
# <a name="sqlprocedures"></a>SQLProcedures
  모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저는 값을 반환합니다. **SQLProcedures** 결과 집합 열 PROCEDURE_TYPE에 대해 sql_pt_function을 합니다.  
  
 **SQLProcedures** 값이 존재 하는지 여부에 관계 없이 SQL_SUCCESS를 반환 *CatalogName, SchemaName* 하거나 *ProcName* 매개 변수입니다. **SQLFetch** 이러한 매개 변수에 잘못 된 값을 사용할 때에 SQL_NO_DATA를 반환 합니다.  
  
 **SQLProcedures** 는 정적 서버 커서에 대해 실행할 수 있습니다. 실행 하려고 **SQLProcedures** 업데이트 가능한 (동적 또는 키 집합) 커서에서 커서 유형이 변경 되었음을 나타내는 sql_success_with_info가 반환 됩니다.  
  
 **SQLProcedures** 이름과 일치 하는 모든 프로시저에 대 한 정보를 반환 *ProcName* 는 현재 사용자에 부여 된 VIEW DEFINITION 권한 또는 현재 사용자가 실행 될 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQLProcedures 함수](https://go.microsoft.com/fwlink/?LinkId=59364)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
