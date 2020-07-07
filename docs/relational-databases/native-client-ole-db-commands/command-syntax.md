---
title: 명령 구문 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, commands
- commands [OLE DB]
- SQL Server Native Client OLE DB provider, stored procedures
- stored procedures [OLE DB], command syntax
ms.assetid: d463d3d7-e5cb-426d-8e92-aa29980356b6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9b882bf54e70a62beeb8ac1ea56a6d3b7913223f
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86002838"
---
# <a name="command-syntax"></a>명령 구문
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 DBGUID_SQL 매크로에 지정 된 명령 구문을 인식 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자의 경우 지정자는 ODBC SQL, ISO 및의 amalgam [!INCLUDE[tsql](../../includes/tsql-md.md)] 가 유효한 구문 임을 나타냅니다. 예를 들어 다음 SQL 문은 ODBC SQL 이스케이프 시퀀스를 사용하여 LCASE 문자열 함수를 지정합니다.  
  
```  
SELECT customerid={fn LCASE(CustomerID)} FROM Customers  
```  
  
 LCASE는 문자열을 반환하고 모든 대문자를 소문자로 변환합니다. ISO 문자열 함수 LOWER도 동일한 작업을 수행하기 때문에 다음 SQL 문은 바로 위에 있는 ODBC 문에 해당하는 ISO 버전입니다.  
  
```  
SELECT customerid=LOWER(CustomerID) FROM Customers  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 명령의 텍스트로 지정 된 경우 문 형식을 성공적으로 처리 합니다.  
  
## <a name="stored-procedures"></a>저장 프로시저  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자 명령을 사용 하 여 저장 프로시저를 실행 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 명령 텍스트에서 ODBC CALL 이스케이프 시퀀스를 사용 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는의 원격 프로시저 호출 메커니즘을 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 명령 처리를 최적화 합니다. 예를 들어 다음 중 [!INCLUDE[tsql](../../includes/tsql-md.md)] 형식보다는 ODBC SQL 문을 명령 텍스트로 사용하는 것이 좋습니다.  
  
-   ODBC SQL  
  
    ```  
    {call SalesByCategory('Produce', '1995')}  
    ```  
  
-   Transact-SQL  
  
    ```  
    EXECUTE SalesByCategory 'Produce', '1995'  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [명령](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
