---
title: 회전 | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2019
ms.prod: sql
ms.reviewer: vanto
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 5420d49b6e5d165168610d002424e3a3b9499748
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411059"
---
# <a name="rotate-enclave-enabled-keys"></a>Enclave 사용 키 회전
[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

Always Encrypted에서 키 회전은 기존 열 마스터 키 또는 열 암호화 키를 새 키로 바꾸는 프로세스입니다. 이 문서에서는 초기 키 및/또는 대상 키(새 키)가 Enclave 사용 키인 경우 [보안 Enclave를 사용한 Always Encrypted](always-encrypted-enclaves.md)와 관련된 키 회전의 사용 사례 및 고려 사항에 관해 설명합니다. Always Encrypted 키 관리에 대한 일반 지침과 프로세스는 [Always Encrypted를 위한 키 관리 개요](overview-of-key-management-for-always-encrypted.md)를 참조하세요. 

보안 또는 규정 준수를 위해 키를 회전해야 할 수도 있습니다. 키가 손상되었거나 조직의 정책에 따라 키를 정기적으로 바꿔야 하는 경우를 예로 들 수 있습니다. 보안 Enclave를 사용한 Always Encrypted 키 회전에서는 암호화된 열에 대한 서버 쪽 보안 Enclave의 기능을 사용하거나 사용하지 않도록 설정하는 방법도 제공합니다.
- Enclave를 사용하지 않는 키를 Enclave 사용 키로 바꾸면 해당 키로 보호되는 열에서 쿼리에 대한 보안 Enclave 기능이 잠금 해제됩니다. [기존 암호화된 열에 관해 보안 Enclave를 사용한 Always Encrypted 사용](always-encrypted-enclaves-enable-for-encrypted-columns.md)을 참조하세요.
 - Enclave 사용 키를 Enclave를 사용하지 않는 키로 바꾸면 해당 키로 보호되는 열에서 쿼리에 대한 보안 Enclave 기능이 사용하지 않도록 설정됩니다.

보안/규정 준수를 위해서만 키를 회전하고 열에 관해 Enclave 계산을 사용하거나 사용하지 않도록 설정하지 않는 경우 대상 키에 원본 키와 동일한 Enclave 관련 구성이 있어야 합니다. 예를 들어 원본 키가 Enclave 사용 키인 경우 대상 키도 Enclave 사용 키여야 합니다.

아래의 개략적인 단계에는 회전 시나리오에 따라 자세한 문서 링크가 포함되어 있습니다.

1. 새 키(열 마스터 키 또는 열 암호화 키)를 프로비저닝합니다.
    - 새 Enclave 사용 키를 프로비저닝하려면 [Enclave 사용 키 프로비저닝](always-encrypted-enclaves-provision-keys.md)을 참조하세요.
    - Enclave를 사용하지 않는 키를 프로비저닝하려면 [SQL Server Management Studio를 사용하여 Always Encrypted 키 프로비저닝](configure-always-encrypted-keys-using-ssms.md) 및 [PowerShell을 사용하여 Always Encrypted 키 프로비저닝](configure-always-encrypted-keys-using-powershell.md)을 참조하세요.
2. 기존 키를 새 키로 바꿉니다.
    - 열 암호화 키를 회전하며 원본 키 및 대상 키 둘 다 Enclave 사용 키인 경우 바로 회전(데이터 다시 암호화 포함)을 실행할 수 있습니다. [보안 enclave를 사용한 Always Encrypted를 이용하여 내부 열 암호화 구성](always-encrypted-enclaves-configure-encryption.md)을 참조하세요.
    - 키 회전에 대한 자세한 단계는 [SQL Server Management Studio를 사용하여 Always Encrypted 키 회전](rotate-always-encrypted-keys-using-ssms.md) 및 [PowerShell을 사용하여 Always Encrypted 키 회전](rotate-always-encrypted-keys-using-powershell.md)을 참조하세요.

    
## <a name="next-steps"></a>다음 단계
- [보안 Enclave를 사용한 Always Encrypted를 사용하여 열 쿼리](always-encrypted-enclaves-query-columns.md)
- [보안 enclave를 사용한 Always Encrypted를 이용하여 내부 열 암호화 구성](always-encrypted-enclaves-configure-encryption.md)
- [기존 암호화된 열에 관해 보안 Enclave를 사용한 Always Encrypted 사용](always-encrypted-enclaves-enable-for-encrypted-columns.md)
- [보안 enclave를 사용한 Always Encrypted를 이용하여 애플리케이션 개발](always-encrypted-enclaves-client-development.md)  

## <a name="see-also"></a>참고 항목  
- [보안 Enclave를 사용한 Always Encrypted 키 관리](always-encrypted-enclaves-manage-keys.md)

