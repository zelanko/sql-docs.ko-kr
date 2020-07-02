---
title: SQLSTATE (ODBC 오류 코드) | Microsoft Docs
description: ODBC 드라이버 SQL Server 저장 프로시저를 원격 저장 프로시저로 실행 하는 경우 프로시저는 정수 반환 코드 및 출력 매개 변수를 사용할 수 있습니다.
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
ms.openlocfilehash: 4efb5bae1383e64bf8b2d13c7f667183e617689d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787969"
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE(ODBC 오류 코드)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  SQLSTATE는 경고 또는 오류의 원인에 대한 자세한 정보를 제공합니다. 에서 검색 되 고 반환 된 데이터 소스에서 발생 하는 오류의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 드라이버는 반환 된 원시 오류 번호를 적절 한 SQLSTATE에 매핑합니다. 네이티브 오류 번호에 매핑할 ODBC 오류 코드가 없는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 드라이버는 SQLSTATE 42000 ("구문 오류 또는 액세스 위반")을 반환 합니다. 드라이버에서 감지한 오류의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 드라이버에서 적절 한 SQLSTATE를 생성 합니다.  
  
 이러한 상태 오류 코드에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [부록 A: ODBC 오류 코드](https://go.microsoft.com/fwlink/?LinkId=89356)  
  
-   [SQLSTATE 매핑(SQLSTATE Mappings)](https://go.microsoft.com/fwlink/?LinkId=89355)  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 메시지 처리](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
