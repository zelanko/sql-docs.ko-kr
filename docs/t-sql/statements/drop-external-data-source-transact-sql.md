---
title: "외부 데이터 원본 (Transact SQL) DROP | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 3f65a2f5-a6c6-4be5-8ca4-6057078fe10e
caps.latest.revision: 14
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3e846395e6bbc5485eecacd70f78b27fc00b005e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-external-data-source-transact-sql"></a>DROP 외부 데이터 원본 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

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
 외부 데이터의 목록을 보려면 원본은 sys.external_data_sources 시스템 뷰를 사용 합니다.  
  
```  
SELECT * FROM sys.external_data_sources;  
```  
  
## <a name="permissions"></a>Permissions  
 필요한 모든 외부 데이터 소스를 변경 합니다.  
  
## <a name="locking"></a>잠금  
 외부 데이터 원본 개체에 대 한 공유 잠금을 사용합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 외부 데이터 원본을 삭제 해도 외부 데이터는 제거 되지 않습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-basic-syntax"></a>1. 기본 구문을 사용 하 여  
  
```  
DROP EXTERNAL DATA SOURCE mydatasource;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-basic-syntax"></a>2. 기본 구문을 사용 하 여  
  
```  
DROP EXTERNAL DATA SOURCE mydatasource;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE EXTERNAL DATA SOURCE&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  


