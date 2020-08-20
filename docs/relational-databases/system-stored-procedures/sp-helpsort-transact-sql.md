---
description: sp_helpsort(Transact-SQL)
title: sp_helpsort (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpsort_TSQL
- sp_helpsort
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpsort
ms.assetid: 2a88d079-3755-43cb-8a54-97d0114149e6
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 22a34a8285a2043159e1bf56191381c6ac933bc5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464175"
---
# <a name="sp_helpsort-transact-sql"></a>sp_helpsort(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 정렬 순서와 문자 집합을 표시합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpsort  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 서버의 기본 데이터 정렬을 반환합니다.  
  
## <a name="remarks"></a>설명  
 의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 설치와 호환 되도록 지정 된 데이터 정렬을 사용 하 여 인스턴스를 설치 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sp_helpsort** 빈 결과를 반환 합니다. 이 동작이 발생할 때 SERVERPROPERTY 개체 (예:)를 쿼리하여 데이터 정렬을 확인할 수 있습니다 `SELECT SERVERPROPERTY ('Collation');` .  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 서버의 기본 정렬 순서 이름, 문자 집합 및 주 정렬 값의 표를 표시하는 방법을 보여 줍니다.  
  
```  
sp_helpsort;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Server default collation`  
  
 `------------------------`  
  
 `Latin1-General, case-sensitive, accent-sensitive, kanatype-insensitive, width-insensitive for Unicode Data, SQL Server Sort Order 51 on Code Page 1252 for non-Unicode Data.`  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 저장 프로시저 ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [COLLATE&#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)   
 [sys.fn_helpcollations&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)   
 [SERVERPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)  
  
  
