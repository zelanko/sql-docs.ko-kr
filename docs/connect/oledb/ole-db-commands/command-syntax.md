---
title: 명령 구문 | Microsoft Docs
description: 명령 구문 및 저장 프로시저
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, commands
- commands [OLE DB]
- OLE DB Driver for SQL Server, stored procedures
- stored procedures [OLE DB], command syntax
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 09c0619e18d1d18d02fd7eddd688c75158fd96f9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="command-syntax"></a>명령 구문
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB Driver for SQL Server는 DBGUID_SQL 매크로로 지정 된 명령 구문을 인식 합니다. OLE DB Driver for SQL Server를 사용할 경우 지정자 하 고 있음을 나타냅니다 ODBC sql, ISO 모두 유효함 및 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 유효한 구문이 있습니다. 예를 들어 다음 SQL 문은 ODBC SQL 이스케이프 시퀀스를 사용하여 LCASE 문자열 함수를 지정합니다.  
  
```  
SELECT customerid={fn LCASE(CustomerID)} FROM Customers  
```  
  
 LCASE는 문자열을 반환하고 모든 대문자를 소문자로 변환합니다. ISO 문자열 함수 LOWER도 동일한 작업을 수행하기 때문에 다음 SQL 문은 바로 위에 있는 ODBC 문에 해당하는 ISO 버전입니다.  
  
```  
SELECT customerid=LOWER(CustomerID) FROM Customers  
```  
  
 OLE DB Driver for SQL Server에는 두 가지 형식의 문 명령 텍스트로 지정 하는 경우에 성공적으로 처리 합니다.  
  
## <a name="stored-procedures"></a>저장 프로시저  
 실행할 때 한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB 드라이버를 사용 하 여 SQL Server 명령에 대 한 저장된 프로시저 명령 텍스트에 ODBC CALL 이스케이프 시퀀스를 사용 합니다. OLE DB Driver for SQL Server의 원격 프로시저 호출 메커니즘에 다음 사용 하 여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 명령 처리를 최적화 합니다. 예를 들어 다음 중 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 형식보다는 ODBC SQL 문을 명령 텍스트로 사용하는 것이 좋습니다.  
  
-   ODBC SQL  
  
    ```  
    {call SalesByCategory('Produce', '1995')}  
    ```  
  
-   Transact-SQL  
  
    ```  
    EXECUTE SalesByCategory 'Produce', '1995'  
    ```  
  
## <a name="see-also"></a>관련 항목:  
 [도구](../../oledb/ole-db-commands/commands.md)  
  
  
