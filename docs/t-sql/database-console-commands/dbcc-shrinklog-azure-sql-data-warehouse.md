---
title: "DBCC SHRINKLOG (Azure SQL 데이터 웨어하우스) | Microsoft Docs"
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
caps.latest.revision: "11"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d06917a784e507ab5568e28b4d34273f5fe71063
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-shrinklog-azure-sql-data-warehouse"></a>DBCC SHRINKLOG (Azure SQL 데이터 웨어하우스)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

트랜잭션 로그의 크기를 줄이는 *기기에서* 현재 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 데이터베이스입니다. 트랜잭션 로그를 축소 하기 위해 데이터 조각화를 방지 합니다. 시간이 지남에 따라 데이터베이스 트랜잭션 로그에는 조각화 하 고 비효율적인 될 수 있습니다. DBCC SHRINKLOG를 사용 하 여 조각화를 줄이고 로그 크기를 줄입니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [TRANSACT-SQL 구문 표기 규칙 &#40; Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DBCC SHRINKLOG   
    [ ( SIZE = { target_size [ MB | GB | TB ]  } | DEFAULT ) ]   
    [ WITH NO_INFOMSGS ]   
[;]  
```  
  
## <a name="arguments"></a>인수  
크기 = { *target_size* [MB | **GB** | TB]} | **기본**합니다.  
*target_size* DBCC SHRINKLOG 완료 된 후 모든 계산 노드에 걸쳐 트랜잭션 로그에 대해 원하는 크기입니다. 0 보다 큰 정수입니다.  
로그 크기 (mb), gb (기가바이트) 또는 tb (테라바이트) 단위로 측정 됩니다. 모든 계산 노드에 트랜잭션 로그의 결합 된 크기는  
기본적으로 DBCC SHRINKLOG이 트랜잭션 로그는 데이터베이스에 대 한 메타 데이터에 저장 된 로그 크기를 줄입니다. 메타 데이터에는 로그 크기의 LOG_SIZE 매개 변수에 따라 사용자가 [CREATE database&#40; Azure SQL 데이터 웨어하우스 &#41; ](../../t-sql/statements/create-database-azure-sql-data-warehouse.md) 또는 [ALTER database&#40; Azure SQL 데이터 웨어하우스 &#41; ](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md). DBCC SHRINKLOG 기본값에 트랜잭션 로그 크기를 줄일 수 시 크기를 `SIZE=DEFAULT` 지정 된 경우 또는 `SIZE` 절을 생략 합니다.
  
WITH NO_INFOMSGS  
정보 메시지는 DBCC SHRINKLOG 결과에 표시 되지 않습니다.  
  
## <a name="permissions"></a>Permissions  
ALTER SERVER STATE 권한이 필요합니다.
  
## <a name="general-remarks"></a>일반적인 주의 사항  
DBCC SHRINKLOG 데이터베이스에 대 한 메타 데이터에 저장 된 로그 크기를 변경 되지 않습니다. 메타 데이터에 CREATE DATABASE 또는 ALTER DATABASE 문에 지정 된 LOG_SIZE 매개 변수를 포함 하도록 계속 합니다.
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-shrink-the-transaction-log-to-the-original-size-specified-by-create-database"></a>1. CREATE DATABASE로 지정 된 원래 크기에 트랜잭션 로그를 축소 합니다.  
주소 데이터베이스를 만들 때 주소 데이터베이스에 대 한 트랜잭션 로그 100MB로 설정 된 가정 합니다. 즉, 주소에 대 한 CREATE DATABASE 문의 했습니다 LOG_SIZE 100MB = 합니다. 이제, 150MB로 로그 증가 했으며 100MB로 다시 작게 축소 하려면 가정해 봅니다.
  
다음 문 중 각는 100MB의 기본 크기를 주소가 데이터베이스에 대 한 트랜잭션 로그를 축소 하려고 합니다. 100MB로 로그를 축소 하면 데이터가 손실 될, 하는 경우 DBCC SHRINKLOG는 데이터 손실 없이 로그를 가능한 가장 작은 크기를 100MB 보다 큰 축소 됩니다.
  
```sql
USE Addresses;  
DBCC SHRINKLOG ( SIZE = 100 MB );  
DBCC SHRINKLOG ( SIZE = DEFAULT );  
DBCC SHRINKLOG;  
```  
  
  
