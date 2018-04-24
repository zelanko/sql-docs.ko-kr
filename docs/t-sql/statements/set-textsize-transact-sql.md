---
title: SET TEXTSIZE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/12/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- TEXTSIZE_TSQL
- TEXTSIZE
- SET_TEXTSIZE_TSQL
- SET TEXTSIZE
dev_langs:
- TSQL
helpviewer_keywords:
- SET TEXTSIZE statement
- SELECT statement [SQL Server], text size returned
- size [SQL Server], text and image data
- TEXTSIZE option
- text size returned [SQL Server]
ms.assetid: 787154a6-39a6-4dd6-a6d0-67b4364f95d5
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 84bfce7530886844d548c9ec3038328482939905
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="set-textsize-transact-sql"></a>SET TEXTSIZE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  SELECT 문에서 반환된 **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **text**, **ntext** 및 **image** 데이터의 크기를 지정합니다.  
  
> [!IMPORTANT]  
>  **ntext**, **text** 및 **image** 데이터 형식은 이후 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 제거됩니다. 향후 개발 작업에서는 이 데이터 형식을 사용하지 않도록 하고 현재 이 데이터 형식을 사용하는 응용 프로그램은 수정하세요. 대신 **nvarchar(max)**, **varchar(max)** 및 **varbinary(max)** 를 사용합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SET TEXTSIZE { number }   
```  
  
## <a name="arguments"></a>인수  
 *number*  
 **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **text**, **ntext** 또는 **image** 데이터의 길이를 바이트 단위로 표시합니다. *숫자*는 최대 값이 2147483647(2GB)인 정수입니다.  값 -1은 무제한 크기를 나타냅니다. 값 0은 크기를 기본값(4KB)으로 다시 설정됩니다.  
  
 연결할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client(10.0 이상) 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 용 ODBC 드라이버가 자동으로 `-1`(무제한)을 지정합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008년보다 오래된  **드라이버:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자(버전 9)는 연결될 때 TEXTSIZE를 2147483647로 자동으로 설정합니다.  
  
## <a name="remarks"></a>Remarks  
 SET TEXTSIZE 설정은 @@TEXTSIZE 함수에 영향을 줍니다.  
  
 SET TEXTSIZE 옵션은 실행 시간 또는 런타임에 설정되며, 구문 분석 시에는 설정되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [@@TEXTSIZE&#40;Transact-SQL&#41;](../../t-sql/functions/textsize-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
