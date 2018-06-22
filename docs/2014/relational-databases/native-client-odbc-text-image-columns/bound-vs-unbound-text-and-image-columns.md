---
title: Vs 바인딩됩니다. Text 및 Image 열에 바인딩되지 않은 | Microsoft Docs
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
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: ffd3442e-d880-46e9-b848-2365a09a2406
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c5129c6b865723721bbb6f176893c950cdf905fe
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082459"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>Vs 바인딩됩니다. 바인딩되지 않은 Text 및 Image 열
  서버 커서를 사용 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 바인딩되지 않은 대 한 데이터를 전송 하지 않도록 최적화 되어 **텍스트**, **ntext**, 또는 **이미지** 열에는 시간 **SQLFetch** 수행 됩니다. **텍스트**, **ntext**, 또는 **이미지** 데이터 실제로에서 검색 되지 않는 서버 응용 프로그램 문제까지 [SQLGetData](../native-client-odbc-api/sqlgetdata.md) 에 열입니다.  
  
 대부분의 응용 프로그램을 작성할 수 있습니다 있도록 없는 **텍스트**, **ntext**, 또는 **이미지** 사용자가 커서에서 위와 아래로 스크롤 하는 동안 데이터가 표시 됩니다. 응용 프로그램이 호출할 수는 사용자가 자세한 내용을 보려면 행을 선택 하면 **SQLGetData** 검색 하는 **텍스트**, **ntext**, 또는 **이미지** 데이터입니다. 이 전송 하지 것입니다는 **텍스트**, **ntext**, 또는 **이미지** 사용자를 선택 하지 않으며 따라서 수 행에 대 한 데이터는 매우 큰 전송 되지 데이터의 총액입니다.  
  
## <a name="see-also"></a>관련 항목  
 [Text 및 Image 열 관리](managing-text-and-image-columns.md)   
 [커서 동작](../native-client-odbc-cursors/cursor-behaviors.md)  
  
  