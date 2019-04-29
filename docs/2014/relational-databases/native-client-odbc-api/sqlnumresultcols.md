---
title: SQLNumResultCols | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLNumResultCols function
ms.assetid: f79d8b3c-521e-4e50-a564-21d73ae5767b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 88edec63a97ff6c463f07add895ff8399fc4268a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63046758"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
  실행된 문의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 결과 집합의 열 수를 보고할 때 서버에 연결하지 않습니다. 이 경우 `SQLNumResultCols` 서버 왕복은 발생 하지 않습니다. 와 같은 [SQLDescribeCol](sqldescribecol.md) 하 고 [SQLColAttribute](sqlcolattribute.md)호출, `SQLNumResultCols` 준비 되었지만 실행된 되지 않은 문에 서버 왕복이 생성 합니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 문 일괄 처리에서 여러 결과 행 집합이 반환되는 경우 결과 집합 열의 수가 하나에서 다른 수로 변경될 수 있습니다. `SQLNumResultCols` 각 집합에 대해 호출 되어야 합니다. 열 수가 변경되면 애플리케이션이 행 결과를 인출하기 전에 데이터 값을 다시 바인딩해야 합니다. 여러 결과 집합 반환을 처리하는 방법은 [SQLMoreResults](sqlmoreresults.md)를 참조하십시오.  
  
 부터 데이터베이스 엔진의 개선 사항 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SQLNumResultCols 예상된 결과 대 한 보다 정확한 설명의 얻을를 허용 합니다. 이전 버전의 SQLNumResultCols 반환한 값에서 다를 수 있습니다 이러한 보다 정확한 결과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 자세한 내용은 [메타데이터 검색](../native-client/features/metadata-discovery.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [SQLNumResultCols 함수](https://go.microsoft.com/fwlink/?LinkId=59359)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  
