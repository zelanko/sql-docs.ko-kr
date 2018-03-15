---
title: DROP EXTERNAL FILE FORMAT(Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
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
ms.assetid: 8cf9009b-59f9-4aac-bef1-dcf2cf0708b2
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 36795146dba75f7bf6a755c1c1ff700b9ed150cd
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="drop-external-file-format-transact-sql"></a>DROP EXTERNAL FILE FORMAT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  PolyBase 외부 파일 형식을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Drop an external file format  
DROP EXTERNAL FILE FORMAT external_file_format_name  
[;]  
```  
  
## <a name="arguments"></a>인수  
 *external_file_format_name*  
 삭제할 외부 파일 형식의 이름입니다.  
  
## <a name="metadata"></a>메타데이터  
 외부 파일 형식 목록을 보려면 [sys.external_file_formats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md) 시스템보기를 사용합니다.  
  
```  
SELECT * FROM sys.external_file_formats;  
```  
  
## <a name="permissions"></a>사용 권한  
 ALTER ANY EXTERNAL FILE FORMAT  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 외부 파일 형식을 삭제해도 외부 데이터는 제거되지 않습니다.  
  
## <a name="locking"></a>잠금  
 외부 파일 형식 개체에 대해 공유 잠금을 적용합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-basic-syntax"></a>1. 기본 구문 사용  
  
```  
DROP EXTERNAL FILE FORMAT myfileformat;  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE EXTERNAL FILE FORMAT&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)  
  
  

