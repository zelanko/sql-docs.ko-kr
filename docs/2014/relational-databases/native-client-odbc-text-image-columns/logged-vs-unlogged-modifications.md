---
title: 기록 및 기록 되지 않는 수정 Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8768acc75d18ea2236f0e9280e5d0c805e688107
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85039374"
---
# <a name="logged-vs-unlogged-modifications"></a>기록되는 수정 및 기록되지 않는 수정
  응용 프로그램에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 드라이버가 **text**, **ntext**및 **image** 를 기록 하지 않도록 요청할 수 있습니다. 하지만 이 옵션을 사용할 때는 주의해야 합니다. **Text**, **ntext**또는 **image** 데이터가 중요 하지 않으며 데이터 소유자가 더 높은 성능을 위해 데이터를 복구 하는 기능을 절충 하는 경우에만 사용 해야 합니다.  
  
 **Text**, **ntext**및 **image** 수정의 로깅은 *특성* 매개 변수를 SQL_SOPT_SS_ TEXTPTR_LOGGING *로 설정 하 고 SQL_TL_OFF* SQL_TL_ON, [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md) 를 호출 하 여 제어 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [text 및 image 열 관리](managing-text-and-image-columns.md)  
  
  
