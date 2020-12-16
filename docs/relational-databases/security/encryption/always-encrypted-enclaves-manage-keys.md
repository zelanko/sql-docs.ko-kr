---
description: 보안 enclave를 사용한 Always Encrypted용 키 관리
title: 보안 enclave를 사용한 Always Encrypted용 키 관리 | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.reviewer: vanto
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15'
ms.openlocfilehash: 0c1f00a5b1e69bdb8f51f848210e8e90b0ae6a4b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477634"
---
# <a name="manage-keys-for-always-encrypted-with-secure-enclaves"></a>보안 enclave를 사용한 Always Encrypted용 키 관리
[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

[보안 enclave를 사용하는 Always Encrypted](always-encrypted-enclaves.md)는 다음 enclave 사용 키를 도입하여 [Always Encrypted](always-encrypted-database-engine.md)용 키 관리를 확장합니다. 

- **Enclave 사용 열 마스터 키** – 데이터베이스 내 열 마스터 키 메타데이터 개체에 `ENCLAVE_COMPUTATIONS` 속성을 지정하여 만든 열 마스터 키입니다. 
- **Enclave 사용 열 암호화 키** – Enclave 사용 열 마스터 키로 암호화된 열 암호화 키입니다. Enclave 사용 열 암호화 키만 서버 쪽 보안 enclave 내에서 계산에 사용할 수 있습니다. 

[Always Encrypted 키 관리에](overview-of-key-management-for-always-encrypted.md)를 위한 일반적인 지침 및 프로세스가 enclave 사용 키 관리에 적용됩니다. 

## <a name="managing-keys"></a>키 관리

다음 문서에서는 enclave 사용 키 관리와 관련된 여러 측면을 설명합니다.

- [Enclave 사용 키 프로비전](always-encrypted-enclaves-provision-keys.md)
- [Enclave 사용 키 순환](always-encrypted-enclaves-rotate-keys.md)

## <a name="next-steps"></a>다음 단계
- [Enclave 사용 키 프로비전](always-encrypted-enclaves-provision-keys.md)

## <a name="see-also"></a>참고 항목  
- [Always Encrypted를 위한 키 관리 개요](overview-of-key-management-for-always-encrypted.md)
- [CREATE COLUMN MASTER KEY(Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
