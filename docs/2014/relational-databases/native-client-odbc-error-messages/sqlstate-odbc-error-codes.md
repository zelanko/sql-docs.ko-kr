---
title: SQLSTATE (ODBC 오류 코드) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- ODBC error handling, cause information
- messages [ODBC], cause information
- SQLSTATEs
- errors [ODBC], cause information
ms.assetid: 84cce528-edb0-473f-a85f-3eb87fbe2cf3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 253841e26ab7ecbeafb2cfeeed8c090c91650d14
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62805867"
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE(ODBC 오류 코드)
  SQLSTATE는 경고 또는 오류의 원인에 대한 자세한 정보를 제공합니다. 에서 검색 되 고 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]된 데이터 소스에서 발생 하는 오류의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native Client ODBC 드라이버는 반환 된 원시 오류 번호를 적절 한 SQLSTATE에 매핑합니다. 네이티브 오류 번호에 매핑할 ODBC 오류 코드가 없는 경우 native Client ODBC 드라이버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLSTATE 42000 ("구문 오류 또는 액세스 위반")을 반환 합니다. 드라이버에서 감지한 오류의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 드라이버에서 적절 한 SQLSTATE를 생성 합니다.  
  
 이러한 상태 오류 코드에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [부록 A: ODBC 오류 코드](https://go.microsoft.com/fwlink/?LinkId=89356)  
  
-   [SQLSTATE 매핑(SQLSTATE Mappings)](https://go.microsoft.com/fwlink/?LinkId=89355)  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 메시지 처리](handling-errors-and-messages.md)  
  
  
