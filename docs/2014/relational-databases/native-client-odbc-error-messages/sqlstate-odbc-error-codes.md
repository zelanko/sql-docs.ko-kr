---
title: SQLSTATE (ODBC 오류 코드) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- ODBC error handling, cause information
- messages [ODBC], cause information
- SQLSTATEs
- errors [ODBC], cause information
ms.assetid: 84cce528-edb0-473f-a85f-3eb87fbe2cf3
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a87719c063e40befb95bc5ce61573dbae8a36325
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37411322"
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE(ODBC 오류 코드)
  SQLSTATE는 경고 또는 오류의 원인에 대한 자세한 정보를 제공합니다. 데이터에서 발생 하는 오류에 대 한 원본 검색 및 반환한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 적절 한 sqlstate 반환 된 원시 오류 번호를 매핑합니다. 원시 오류 번호를 매핑할 ODBC 오류 코드가 없는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 SQLSTATE 42000 ("구문 오류 또는 액세스 위반 입니다")를 반환 합니다. 드라이버에 의해 검색 되는 오류는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 적절 한 SQLSTATE를 생성 합니다.  
  
 이러한 상태 오류 코드에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [부록 A: ODBC 오류 코드](http://go.microsoft.com/fwlink/?LinkId=89356)  
  
-   [SQLSTATE 매핑](http://go.microsoft.com/fwlink/?LinkId=89355)  
  
## <a name="see-also"></a>관련 항목  
 [오류 및 메시지 처리](handling-errors-and-messages.md)  
  
  
