---
description: HOST_ID(Transact-SQL)
title: HOST_ID(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- HOST_ID
- HOST_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IDs [SQL Server], workstations
- HOST_ID function
- workstation IDs [SQL Server]
- identification numbers [SQL Server], workstations
ms.assetid: 36ba56d4-20d7-4cd1-aa2a-e40a6c0a4e39
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 099026a22a03c563b8ea176d5fed14d7d936ffc6
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91116346"
---
# <a name="host_id-transact-sql"></a>HOST_ID(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  워크스테이션 ID 번호를 반환합니다. 워크스테이션 ID 번호는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결된 클라이언트 컴퓨터에 있는 애플리케이션의 PID(프로세스 ID)입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
HOST_ID ()  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 **char(10)**  
  
## <a name="remarks"></a>설명  
 시스템 함수의 매개 변수가 선택 사항이면 현재 데이터베이스, 호스트 컴퓨터, 서버 사용자 또는 데이터베이스 사용자를 가정합니다. 기본 제공 함수 다음에는 항상 괄호가 와야 합니다.  
  
 시스템 함수는 선택 목록, WHERE 절 및 식이 허용되는 모든 곳에서 사용될 수 있습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 주문 정보를 기록하는 테이블을 만들고 컴퓨터의 터미널 ID를 기록하는 행의 `HOST_ID()` 정의에 `DEFAULT`를 사용합니다.  
  
```sql  
CREATE TABLE Orders  
   (OrderID     INT       PRIMARY KEY,  
    CustomerID  NCHAR(5)  REFERENCES Customers(CustomerID),  
    TerminalID  CHAR(8)   NOT NULL DEFAULT HOST_ID(),  
    OrderDate   DATETIME  NOT NULL,  
    ShipDate    DATETIME  NULL,  
    ShipperID   INT       NULL REFERENCES Shippers(ShipperID));  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
  
  
