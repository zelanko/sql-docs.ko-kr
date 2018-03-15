---
title: DROP EXTERNAL DATA SOURCE(Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 3f65a2f5-a6c6-4be5-8ca4-6057078fe10e
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b479c5fd28b97eb6fae75d9490a52c9e56c3fa7f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="drop-external-data-source-transact-sql"></a>DROP EXTERNAL DATA SOURCE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  PolyBase 외부 데이터 원본을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Drop an external data source  
DROP EXTERNAL DATA SOURCE external_data_source_name  
[;]  
```  
  
## <a name="arguments"></a>인수  
 *external_data_source_name*  
 삭제할 외부 데이터 원본의 이름입니다.  
  
## <a name="metadata"></a>메타데이터  
 외부 데이터 원본의 목록을 보려면 external_data_sources 시스템 뷰를 사용합니다.  
  
```  
SELECT * FROM sys.external_data_sources;  
```  
  
## <a name="permissions"></a>사용 권한  
 ALTER ANY EXTERNAL DATA SOURCE가 필요합니다.  
  
## <a name="locking"></a>잠금  
 외부 데이터 원본 개체에 대해 공유 잠금을 적용합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 외부 데이터 원본을 삭제해도 외부 데이터는 제거되지 않습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-basic-syntax"></a>1. 기본 구문 사용  
  
```  
DROP EXTERNAL DATA SOURCE mydatasource;  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE EXTERNAL DATA SOURCE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  

