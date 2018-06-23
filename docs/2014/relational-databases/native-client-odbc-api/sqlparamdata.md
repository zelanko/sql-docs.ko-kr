---
title: SQLParamData | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLParamData function
ms.assetid: 92349482-ea22-4a6a-8484-e9c6566794fa
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: bd3fefeaa05f806650b58d1778658fda0ed63fa2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092867"
---
# <a name="sqlparamdata"></a>SQLParamData
  SQLParamData 반환 하는 경우는 *ValuePtrPtr* 와 연결 된 테이블 반환 매개 변수는 응용 프로그램 호출 해야와 SQLPutData *StrLen_Or_Ind*합니다. 경우 *StrLen_Or_Ind* 0 보다 큰 값이 응용 프로그램에 대 한 준비 되었음을 의미 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 다음 테이블 반환 매개 변수 행에 대 한 매개 변수 데이터를 수집 합니다. *StrLen_Or_Ind* 의 값이 0이면 테이블 반환 매개 변수에 대한 데이터의 행이 더 이상 없음을 나타냅니다. 자세한 내용은 참조 [바인딩 및 Data Transfer of Table-Valued 매개 변수 및 열 값](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md)합니다.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 참조 [테이블 반환 매개 변수 &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQLParamData](http://go.microsoft.com/fwlink/?LinkId=80706)   
 [ODBC API 구현 정보](odbc-api-implementation-details.md)  
  
  