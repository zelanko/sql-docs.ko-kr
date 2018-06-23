---
title: 검색 결과 집합 정보 (ODBC) | Microsoft Docs
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
- result sets [ODBC]
- result sets [ODBC], fetching
ms.assetid: 34f235e4-f80b-4123-8764-9deb18506f14
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ae6d8f1c5640ee0dc8f63b54a2117057b8f334e2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090641"
---
# <a name="retrieve-result-set-information-odbc"></a>결과 집합 정보 검색(ODBC)
    
### <a name="to-get-information-about-a-result-set"></a>결과 집합에 대한 정보를 가져오려면  
  
1.  호출 [SQLNumResultCols](../native-client-odbc-api/sqlnumresultcols.md) 결과 집합의 열 개수를 가져올 수 있습니다.  
  
2.  결과 집합의 각 열에 대해 다음을 수행합니다.  
  
    -   호출 [SQLDescribeCol](../native-client-odbc-api/sqldescribecol.md) 결과 열에 대 한 정보를 얻을 수 있습니다.  
  
     또는  
  
    -   호출 [SQLColAttribute](../native-client-odbc-api/sqlcolattribute.md) 결과 열에 대 한 특정 설명자 정보를 가져올 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [결과 처리 방법 도움말 항목 &#40;ODBC&#41;](../../database-engine/dev-guide/processing-results-how-to-topics-odbc.md)   
 [결과 집합의 특징을 확인 &#40;ODBC&#41;](../native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  