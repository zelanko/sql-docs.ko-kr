---
title: Always Encrypted 서버 구성 옵션에 대한 Enclave 형식 구성 | Microsoft Docs
description: Always Encrypted의 보안 Enclave를 사용하거나 사용하지 않는 방법을 알아봅니다. Enclave가 올바르게 초기화되었는지 확인하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15'
ms.openlocfilehash: 45f6bdca2602a9a85cf9fc193269b445599c78ad
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97480334"
---
# <a name="configure-the-enclave-type-for-always-encrypted-server-configuration-option"></a>Always Encrypted 서버 구성 옵션에 대한 Enclave 형식 구성

[!INCLUDE [sqlserver2019-windows-only](../../includes/applies-to-version/sqlserver2019-windows-only.md)]

이 문서에서는 보안 Enclave를 사용한 Always Encrypted에 관해 보안 Enclave를 사용하거나 사용하지 않도록 설정하는 방법을 설명합니다. 자세한 내용은 [보안 Enclave를 사용한 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)를 참조하세요.

**열 암호화 Enclave 형식** 서버 구성 옵션은 Always Encrypted에 사용되는 보안 Enclave의 형식을 제어합니다. 옵션은 다음 값 중 하나로 설정할 수 있습니다.  
  
|값|Description|  
|-------------------|-----------------| 
|0|**보안 Enclave 없음** [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 Always Encrypted의 보안 Enclave를 초기화하지 않습니다. 결과적으로, 보안 Enclave를 사용한 Always Encrypted를 사용할 수 없게 됩니다.|  
|1|**VBS(가상화 기반 보안)** [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 VBS(가상화 기반 보안) Enclave 초기화를 시도합니다.

> [!IMPORTANT]
> **열 암호화 Enclave 형식** 변경 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 다시 시작해야만 적용됩니다.
   
[sys.configurations(Transact-SQL)](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) 뷰를 사용하여 구성된 Enclave 형식 값과 현재 적용되는 Enclave 형식 값을 확인할 수 있습니다. 

[!INCLUDE [ssnoversion-md](../../includes/ssnoversion-md.md)]를 마지막으로 다시 시작한 후 현재 적용되는 형식의 Enclave(0보다 큼)가 올바르게 초기화되었는지 확인하려면 다음과 같이 [sys.dm_column_encryption_enclave(Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-column-encryption-enclave.md) 뷰를 확인합니다.
 - 뷰에 정확히 하나의 행이 있으면 Enclave가 올바르게 초기화된 것입니다. 
 - 뷰에 행이 없으면 SQL Server 오류 로그에서 Enclave 초기화 오류를 확인합니다. [SQL Server 오류 로그 보기(SQL Server Management Studio)](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)를 참조하세요.

VBS Enclave 구성 방법에 대한 단계별 지침은 [SQL Server에서 보안 Enclave를 사용한 Always Encrypted 사용](../../relational-databases/security/tutorial-getting-started-with-always-encrypted-enclaves.md#step-3-enable-always-encrypted-with-secure-enclaves-in-sql-server)을 참조하세요.

## <a name="examples"></a>예제  
 다음 예제에서는 보안 Enclave를 사용하도록 설정하고 Enclave 형식을 VBS로 설정합니다.

```sql  
sp_configure 'column encryption enclave type', 1;  
GO  
RECONFIGURE;  
GO  
```  

다음 예제에서는 보안 Enclave를 사용하지 않도록 설정합니다.  

```sql  
sp_configure 'column encryption enclave type', 0;  
GO  
RECONFIGURE;  
GO  
```  

다음 쿼리는 구성된 Enclave 형식과 현재 적용되는 Enclave 형식을 검색합니다.

```sql  
USE [master];
GO
SELECT
[value]
, CASE [value] WHEN 0 THEN 'No enclave' WHEN 1 THEN 'VBS' ELSE 'Other' END AS [value_description]
, [value_in_use]
, CASE [value_in_use] WHEN 0 THEN 'No enclave' WHEN 1 THEN 'VBS' ELSE 'Other' END AS [value_in_use_description]
FROM sys.configurations
WHERE [name] = 'column encryption enclave type'; 
```  
## <a name="next-steps"></a>다음 단계
 [보안 Enclave를 사용한 Always Encrypted 키 관리](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)

## <a name="see-also"></a>참고 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [sys.configurations(Transact-SQL)](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [sys.dm_column_encryption_enclave(Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-column-encryption-enclave.md)   
