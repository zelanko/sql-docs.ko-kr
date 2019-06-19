---
title: 열 암호화 Enclave 형식 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
manager: jroth
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 1031bdfa3aa6c728d3e33b500fe942d5e52c5fdc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66799472"
---
# <a name="column-encryption-enclave-type-server-configuration-option"></a>열 암호화 Enclave 형식 서버 구성 옵션
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  **열 암호화 Enclave 형식** 옵션을 사용하여 Always Encrypted의 보안 Enclave를 사용하거나 사용하지 않도록 설정합니다.  자세한 내용은 [보안 Enclave를 사용한 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)를 참조하세요.

 다음 표에는 사용 가능한 **열 암호화 Enclave 형식** 값이 나와 있습니다.  
  
|값|설명|  
|-------------------|-----------------|  
|0|**보안 Enclave 없음** [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 Always Encrypted의 보안 Enclave를 초기화하지 않습니다. 결과적으로, 보안 Enclave를 사용한 Always Encrypted를 사용할 수 없게 됩니다.|  
|1|**VBS(가상화 기반 보안)** [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 Always Encrypted의 보안 Enclave(VBS 보안 메모리 Enclave)를 초기화합니다.|    

> [!IMPORTANT]
> **열 암호화 Enclave 형식** 변경 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 다시 시작해야만 적용됩니다.
  
   
## <a name="examples"></a>예  
 다음 예제에서는 보안 Enclave를 사용하도록 설정합니다.  

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

## <a name="see-also"></a>참고 항목  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
