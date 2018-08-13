---
title: sp_helpsort (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helpsort_TSQL
- sp_helpsort
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpsort
ms.assetid: 2a88d079-3755-43cb-8a54-97d0114149e6
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: b72de312f8d3ab7abadc592b14149d47f65dfa7a
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39539413"
---
# <a name="sphelpsort-transact-sql"></a>sp_helpsort(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 정렬 순서와 문자 집합을 표시합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpsort  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 서버의 기본 데이터 정렬을 반환합니다.  
  
## <a name="remarks"></a>Remarks  
 인스턴스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 이전 설치와 호환 되도록 지정 된 데이터 정렬으로 설치 되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **sp_helpsort** 빈 결과 반환 합니다. 이 동작이 발생 하면 같은 SERVERPROPERTY 개체를 쿼리하여 데이터 정렬을 확인할 수 있습니다: `SELECT SERVERPROPERTY ('Collation');`합니다.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 서버의 기본 정렬 순서 이름, 문자 집합 및 주 정렬 값의 표를 표시하는 방법을 보여 줍니다.  
  
```  
sp_helpsort;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Server default collation`  
  
 `------------------------`  
  
 `Latin1-General, case-sensitive, accent-sensitive, kanatype-insensitive, width-insensitive for Unicode Data, SQL Server Sort Order 51 on Code Page 1252 for non-Unicode Data.`  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터베이스 엔진 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [COLLATE&#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)   
 [sys.fn_helpcollations&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)   
 [SERVERPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)  
  
  
