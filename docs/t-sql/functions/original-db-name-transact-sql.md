---
title: ORIGINAL_DB_NAME (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ORIGINAL_DB_NAME
- ORIGINAL_DB_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ORIGINAL_DB_NAME function
ms.assetid: 7dadc40a-1287-4f31-8487-434ee477144d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1779494dce49c9b36fa1f98cffea65f4716ab00d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="originaldbname-transact-sql"></a>ORIGINAL_DB_NAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  사용자가 데이터베이스 연결 문자열에 지정한 데이터베이스 이름을 반환합니다. 이 사용 하 여 지정 된 데이터베이스는 **sqlcmd-d** 옵션 (사용 하 여 *데이터베이스*) 또는 ODBC 데이터 원본 식 (초기 카탈로그 =*databasename*).  
  
 이 데이터베이스는 기본 사용자 데이터베이스와 같습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
ORIGINAL_DB_NAME ()  
```  
  
## <a name="remarks"></a>주의  
 초기 데이터베이스가 지정되지 않았으면 함수는 빈 문자열을 반환합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sqlcmd 유틸리티](../../tools/sqlcmd-utility.md)   
 [osql 유틸리티](../../tools/osql-utility.md)   
 [SQL Server Native Client &#40; ODBC &#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
