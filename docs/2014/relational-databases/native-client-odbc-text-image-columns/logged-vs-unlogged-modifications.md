---
title: 로깅된 vs입니다. 수정 기록 되지 않는 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- logged vs. nonlogged modifications [SQL Server Native Client]
- columns [ODBC]
- ODBC data types, image columns
- nonlogged vs. logged modifications
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 20aa5b27-4a2c-46e7-8356-beb0eebf4b7e
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d5c73288c57a834008f4d09ad098ad1b41183e76
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36186973"
---
# <a name="logged-vs-unlogged-modifications"></a>로깅된 vs입니다. 기록 되지 않는 수정
  응용 프로그램 않도록 요청할 수 있습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 로그 아님 **텍스트**, **ntext**, 및 **이미지** 수정 합니다. 하지만 이 옵션을 사용할 때는 주의해야 합니다. 경우에만 사용 해야 여기서는 **텍스트**, **ntext**, 또는 **이미지** 데이터가 중요 하지 않으며 데이터 소유자는 기꺼이 포기에 대 한 데이터를 복구 하는 기능 성능 향상  
  
 로깅을 **텍스트**, **ntext**, 및 **이미지** 수정 작업을 호출 하 여 제어 [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md) 와  *특성* 매개 변수 SQL_SOPT_SS_ TEXTPTR_LOGGING로 설정 하 고 *ValuePtr* SQL_TL_ON 또는 SQL_TL_OFF로 설정 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [text 및 image 열 관리](managing-text-and-image-columns.md)  
  
  