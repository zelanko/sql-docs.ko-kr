---
title: 명령 구문 | Microsoft Docs
description: 명령 구문 및 저장 프로시저
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-commands
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
ms.openlocfilehash: 8e7fab68cc4a945bc34c64b2b832b182c734d927
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2018
ms.locfileid: "39105939"
---
# <a name="command-syntax"></a>명령 구문
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server는 DBGUID_SQL 매크로로 지정 된 명령 구문을 인식 합니다. OLE DB 드라이버의 SQL Server에 대 한 경우 지정자를 나타냅니다 ODBC sql, ISO 모두 유효함 및 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 올바른 구문입니다. 예를 들어 다음 SQL 문은 ODBC SQL 이스케이프 시퀀스를 사용하여 LCASE 문자열 함수를 지정합니다.  
  
```  
SELECT customerid={fn LCASE(CustomerID)} FROM Customers  
```  
  
 LCASE는 문자열을 반환하고 모든 대문자를 소문자로 변환합니다. ISO 문자열 함수 LOWER도 동일한 작업을 수행하기 때문에 다음 SQL 문은 바로 위에 있는 ODBC 문에 해당하는 ISO 버전입니다.  
  
```  
SELECT customerid=LOWER(CustomerID) FROM Customers  
```  
  
 명령 텍스트로 지정할 경우 SQL Server용 OLE DB 드라이버는 위의 두 가지 명령문 형식 모두를 문제 없이 처리합니다.  
  
## <a name="stored-procedures"></a>저장 프로시저  
 SQL Server용 OLE DB 드라이버 명령을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 저장 프로시저를 실행할 경우 명령 텍스트에 ODBC CALL 이스케이프 시퀀스를 사용해야 합니다. SQL Server용 OLE DB 드라이버는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 원격 프로시저 호출 메커니즘을 사용하여 명령 처리를 최적화합니다. 예를 들어 다음 중 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 형식보다는 ODBC SQL 문을 명령 텍스트로 사용하는 것이 좋습니다.  
  
-   ODBC SQL  
  
    ```  
    {call SalesByCategory('Produce', '1995')}  
    ```  
  
-   Transact-SQL  
  
    ```  
    EXECUTE SalesByCategory 'Produce', '1995'  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [도구](../../oledb/ole-db-commands/commands.md)  
  
  
