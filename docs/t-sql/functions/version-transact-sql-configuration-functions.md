---
description: '&#x40;&#x40;버전 - Transact SQL 구성 함수'
title: '@@VERSION(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/20/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@VERSION'
- '@@VERSION_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@VERSION function'
- current SQL Server installation information
- versions [SQL Server], @@VERSION
- processors [SQL Server], types
ms.assetid: 385ba80e-7c28-41a5-9cdb-5648f3785983
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7670a4e4cdb412ad55bfef01f8322c37023335e2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97422455"
---
# <a name="x40x40version---transact-sql-configuration-functions"></a>&#x40;&#x40;버전 - Transact SQL 구성 함수
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 현재 설치에 대한 시스템 및 빌드 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
@@VERSION  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 **nvarchar**  
  
## <a name="remarks"></a>설명  
 @@VERSION 결과는 하나의 nvarchar 문자열로 표시됩니다. [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md) 함수를 사용하여 개별 속성 값을 검색할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 경우 다음 정보가 반환됩니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전  
  
-   프로세서 아키텍처  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 빌드 날짜  
  
-   저작권 공지  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전  
  
-   운영 체제 버전  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]의 경우 다음 정보가 반환됩니다.  
  
-   버전- "Microsoft SQL Azure"  
  
-   제품 수준- "(RTM)"  
  
-   제품 버전  
  
-   빌드 날짜  
  
-   저작권 공지  

> [!NOTE]  
> @@VERSION에서 보고한 제품 버전이 Azure SQL Database에 올바르지 않은 문제를 알고 있습니다. Azure SQL Database에서 실행하는 SQL Server 데이터베이스 엔진의 버전은 SQL Server의 온-프레미스 이상 버전으로 최신 보안 수정이 포함되어 있습니다. 즉, 패치 수준이 항상 SQL Server의 온-프레미스 버전 이상으로 SQL Server에서 사용할 수 있는 최신 기능이 Azure SQL Database에서 제공됩니다.
>
> 엔진 버전을 프로그래밍 방식으로 결정하려면 SELECT SERVERPROPERTY('EngineEdition')를 사용합니다. 이 쿼리는 Azure SQL Database에 대해 ‘5’를 반환하고 Azure SQL Managed Instance에 대해 ‘8’을 반환합니다.
>
> 이 문제를 해결한 후에 설명서를 업데이트할 예정입니다.

  
## <a name="examples"></a>예  
  
### <a name="a-return-the-current-version-of-ssnoversion"></a>1\. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 현재 버전 반환  
 다음 예에서는 현재 설치의 버전 정보를 반환합니다.  
  
```sql
SELECT @@VERSION AS 'SQL Server Version';  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-return-the-current-version-of-ssdw"></a>B. [!INCLUDE[ssDW](../../includes/ssdw-md.md)]의 현재 버전 반환  
  
```sql
SELECT @@VERSION AS 'SQL Server PDW Version';  
```  
  
## <a name="see-also"></a>참고 항목  
 [SERVERPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)  
  
  

