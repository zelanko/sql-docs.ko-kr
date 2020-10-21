---
description: 보안 함수(Transact-SQL)
title: 보안 함수(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], security
- security functions
- roles [SQL Server], functions
- users [SQL Server], security functions
- security [SQL Server], functions
ms.assetid: 7773a87d-2f1b-4951-a225-baf159a7291b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 47e88bb71ac656debf02646a99e51ca77ab243c6
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037448"
---
# <a name="security-functions-transact-sql"></a>보안 함수(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  다음 보안 함수는 보안 관리에 유용한 정보를 반환합니다. 추가 기능은 [암호화 함수&#40;Transact-SQL&#41;](../../t-sql/functions/cryptographic-functions-transact-sql.md)에 나열되어 있습니다.  
  
:::row:::
    :::column:::
        [CERTENCODED &#40;Transact-SQL&#41;](../../t-sql/functions/certencoded-transact-sql.md)
    :::column-end:::
    :::column:::
        [PWDCOMPARE &#40;Transact-SQL&#41;](../../t-sql/functions/pwdcompare-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md)
    :::column-end:::
    :::column:::
        [PWDENCRYPT &#40;Transact-SQL&#41;](../../t-sql/functions/pwdencrypt-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [CURRENT_USER &#40;Transact-SQL&#41;](../../t-sql/functions/current-user-transact-sql.md)
    :::column-end:::
    :::column:::
        [SCHEMA_ID&#40;Transact-SQL&#41;](../../t-sql/functions/schema-id-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [DATABASE_PRINCIPAL_ID &#40;Transact-SQL&#41;](../../t-sql/functions/database-principal-id-transact-sql.md)
    :::column-end:::
    :::column:::
        [SCHEMA_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/schema-name-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sys.fn_builtin_permissions&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)
    :::column-end:::
    :::column:::
        [SESSION_USER &#40;Transact-SQL&#41;](../../t-sql/functions/session-user-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sys.fn_get_audit_file&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)
    :::column-end:::
    :::column:::
        [SUSER_ID &#40;Transact-SQL&#41;](../../t-sql/functions/suser-id-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)
    :::column-end:::
    :::column:::
        [SUSER_SID &#40;Transact-SQL&#41;](../../t-sql/functions/suser-sid-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [HAS_PERMS_BY_NAME&#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)
    :::column-end:::
    :::column:::
        [SUSER_SNAME&#40;Transact-SQL&#41;](../../t-sql/functions/suser-sname-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [IS_MEMBER&#40;Transact-SQL&#41;](../../t-sql/functions/is-member-transact-sql.md)
    :::column-end:::
    :::column:::
        [SYSTEM_USER &#40;Transact-SQL&#41;](../../t-sql/functions/system-user-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [IS_ROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-rolemember-transact-sql.md)
    :::column-end:::
    :::column:::
        [SUSER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/suser-name-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [IS_SRVROLEMEMBER&#40;Transact-SQL&#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)
    :::column-end:::
    :::column:::
        [USER_ID &#40;Transact-SQL&#41;](../../t-sql/functions/user-id-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [ORIGINAL_LOGIN &#40;Transact-SQL&#41;](../../t-sql/functions/original-login-transact-sql.md)
    :::column-end:::
    :::column:::
        [USER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/user-name-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [PERMISSIONS &#40;Transact-SQL&#41;](../../t-sql/functions/permissions-transact-sql.md)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

&nbsp;
  
 Windows 그룹의 구성원 자격에 대한 자세한 내용은 [xp_logininfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md) 및 [xp_enumgroups &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-enumgroups-transact-sql.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [암호화 함수&#40;Transact-SQL&#41;](../../t-sql/functions/cryptographic-functions-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [보안 문](../statements/permissions-grant-deny-revoke-azure-sql-data-warehouse-parallel-data-warehouse.md)  
  
