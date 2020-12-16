---
title: In-Memory OUTER JOIN | Microsoft Docs
description: 왼쪽 및 오른쪽 우선 외부 조인에 대해 알아봅니다. 고유하게 컴파일된 T-SQL 모듈은 SQL Server에서 왼쪽 및 오른쪽 우선 외부 조인을 지원합니다.
ms.custom: ''
ms.date: 06/01/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 67084043-6b23-4975-b9db-6e49923d4bab
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 169270645374ecad9a9faf65cac23b4e178d1bdc
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460466"
---
# <a name="implementing-an-outer-join"></a>외부 조인 구현

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 고유하게 컴파일된 T-SQL 모듈에서 LEFT 및 RIGHT OUTER JOIN이 지원됩니다.  
  
OUTER JOIN에 대한 자세한 내용은 [FROM 절과 JOIN, APPLY, PIVOT](../../t-sql/queries/from-transact-sql.md)을 참조하세요.
