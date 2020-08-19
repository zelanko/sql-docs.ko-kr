---
description: PWDENCRYPT(Transact-SQL)
title: PWDENCRYPT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PWDENCRYPT
- PWDENCRYPT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PWDENCRYPT function [Transact-SQL]
ms.assetid: 333e9a43-1099-4b9b-b941-4b0b016f47f3
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0b25d123f34de28d64e39e3593f918e01eada30b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88445595"
---
# <a name="pwdencrypt-transact-sql"></a>PWDENCRYPT(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  암호 해시 알고리즘의 현재 버전을 사용하는 입력 값의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 암호 해시를 반환합니다.  
  
 PWDENCRYPT는 오래된 함수로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이후 릴리스에서는 지원되지 않을 수 있습니다. 대신 [HASHBYTES](../../t-sql/functions/hashbytes-transact-sql.md)를 사용합니다. HASHBYTES는 더 많은 해시 알고리즘을 제공합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
PWDENCRYPT ( 'password' )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *password*  
 암호화할 암호입니다. *암호*는 **sysname**입니다.  
  
## <a name="return-types"></a>반환 형식  
 **varbinary(128)**  
  
## <a name="permissions"></a>사용 권한  
 PWDENCRYPT는 누구나 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [PWDCOMPARE &#40;Transact-SQL&#41;](../../t-sql/functions/pwdcompare-transact-sql.md)  
  
  
