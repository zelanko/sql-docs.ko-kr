---
description: HOST_NAME(Transact-SQL)
title: HOST_NAME(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- HOST_NAME_TSQL
- HOST_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- HOST_NAME function
- workstation names [SQL Server]
ms.assetid: 4b8b0705-c083-4b07-b954-c83ee73b2ebb
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 3dbd0179163a13989308f1c01ba350b37bf959ea
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91116684"
---
# <a name="host_name-transact-sql"></a>HOST_NAME(Transact-SQL)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  워크스테이션 이름을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
HOST_NAME ()  
```  

## <a name="return-types"></a>반환 형식
 **nvarchar(128)**  
  
## <a name="remarks"></a>설명  
 시스템 함수의 매개 변수가 선택 사항이면 현재 데이터베이스, 호스트 컴퓨터, 서버 사용자 또는 데이터베이스 사용자를 가정합니다. 기본 제공 함수 다음에는 항상 괄호가 와야 합니다.  
  
 시스템 함수는 선택 목록, WHERE 절 및 식이 허용되는 모든 곳에서 사용될 수 있습니다.  
  
> [!IMPORTANT]  
>  클라이언트 애플리케이션에서 워크스테이션 이름을 제공하므로 제공된 데이터가 정확하지 않을 수 있습니다. HOST_NAME을 보안 용도로는 사용하지 마세요.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `HOST_NAME()` 정의에 `DEFAULT`을 사용하는 테이블을 만들고 주문 기록 테이블에 행을 삽입하는 컴퓨터의 워크스테이션 이름을 새로 만든 테이블에 기록합니다.  
  
```sql  
CREATE TABLE Orders  
   (OrderID     INT        PRIMARY KEY,  
    CustomerID  NCHAR(5)   REFERENCES Customers(CustomerID),  
    Workstation NCHAR(30)  NOT NULL DEFAULT HOST_NAME(),  
    OrderDate   DATETIME   NOT NULL,  
    ShipDate    DATETIME   NULL,  
    ShipperID   INT        NULL REFERENCES Shippers(ShipperID));  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
  
  
