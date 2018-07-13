---
title: Vs를 기록된 합니다. 수정 기록 되지 않는 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 34064aaa2e96a7d610f8709c1f5750bddd62b766
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37420304"
---
# <a name="logged-vs-unlogged-modifications"></a>Vs를 기록된 합니다. 기록 되지 않는 수정
  응용 프로그램에서 요청 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 로그 아님 **텍스트**를 **ntext**, 및 **이미지** 수정 합니다. 하지만 이 옵션을 사용할 때는 주의해야 합니다. 경우에만 사용 해야 여기서 합니다 **텍스트**를 **ntext**, 또는 **이미지** 데이터가 중요 하지 않으며 데이터 소유자가 데이터를 복구 하는 기능 기꺼이 성능 향상  
  
 로깅을 **텍스트**, **ntext**, 및 **이미지** 호출 하 여 수정 제어 [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md) 사용 하 여는  *특성* 매개 변수 SQL_SOPT_SS_ TEXTPTR_LOGGING로 설정 하 고 *ValuePtr* 변수와 SQL_TL_ON 또는 SQL_TL_OFF로 설정 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [text 및 image 열 관리](managing-text-and-image-columns.md)  
  
  
