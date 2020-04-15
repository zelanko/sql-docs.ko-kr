---
title: SQLSTATE (ODBC 오류 코드) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8c7f3fbdf690989830cff2a41028ee0c1e2c9f37
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291534"
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE(ODBC 오류 코드)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQLSTATE는 경고 또는 오류의 원인에 대한 자세한 정보를 제공합니다. 에서 검색되고 반환되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]데이터 원본에서 발생하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류의 경우 네이티브 클라이언트 ODBC 드라이버는 반환된 기본 오류 번호를 해당 SQLSTATE에 매핑합니다. 기본 오류 번호에 매핑할 ODBC 오류 코드가 없는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 경우 네이티브 클라이언트 ODBC 드라이버는 SQLSTATE 42000("구문 오류 또는 액세스 위반")을 반환합니다. 드라이버에서 검색되는 오류의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 경우 네이티브 클라이언트 ODBC 드라이버는 적절한 SQLSTATE를 생성합니다.  
  
 이러한 상태 오류 코드에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [부록 A: ODBC 오류 코드](https://go.microsoft.com/fwlink/?LinkId=89356)  
  
-   [SQLSTATE 매핑(SQLSTATE Mappings)](https://go.microsoft.com/fwlink/?LinkId=89355)  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 메시지 처리](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
