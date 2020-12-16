---
description: DROP EXTERNAL DATA SOURCE(Transact-SQL)
title: DROP EXTERNAL DATA SOURCE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 3f65a2f5-a6c6-4be5-8ca4-6057078fe10e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 797a416934de76f2154d084c8a4bf964cd611c91
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478504"
---
# <a name="drop-external-data-source-transact-sql"></a>DROP EXTERNAL DATA SOURCE(Transact-SQL)
[!INCLUDE [sqlserver2016-asdbmi-asa-pdw](../../includes/applies-to-version/sqlserver2016-asdbmi-asa-pdw.md)]

  PolyBase 외부 데이터 원본을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
-- Drop an external data source  
DROP EXTERNAL DATA SOURCE external_data_source_name  
[;]  
```  
  
## <a name="arguments"></a>인수  
 *external_data_source_name*  
 삭제할 외부 데이터 원본의 이름입니다.  
  
## <a name="metadata"></a>메타데이터  
 외부 데이터 원본의 목록을 보려면 external_data_sources 시스템 뷰를 사용합니다.  
  
```sql  
SELECT * FROM sys.external_data_sources;  
```  
  
## <a name="permissions"></a>사용 권한  
 ALTER ANY EXTERNAL DATA SOURCE가 필요합니다.  
  
## <a name="locking"></a>잠금  
 외부 데이터 원본 개체에 대해 공유 잠금을 적용합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 외부 데이터 원본을 삭제해도 외부 데이터는 제거되지 않습니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-using-basic-syntax"></a>A. 기본 구문 사용  
  
```sql  
DROP EXTERNAL DATA SOURCE mydatasource;  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE EXTERNAL DATA SOURCE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  

