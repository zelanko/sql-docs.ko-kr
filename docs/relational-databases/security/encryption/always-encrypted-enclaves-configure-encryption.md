---
description: 보안 Enclave를 사용한 Always Encrypted를 사용하여 바로 열 암호화 구성
title: 보안 Enclave를 사용한 Always Encrypted를 사용하여 바로 열 암호화 구성 | Microsoft Docs
ms.custom: ''
ms.date: 10/10/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: bb922b1dc85706e0630dd3d67dcb33459c490124
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91863699"
---
# <a name="configure-column-encryption-in-place-using-always-encrypted-with-secure-enclaves"></a>보안 Enclave를 사용한 Always Encrypted를 사용하여 바로 열 암호화 구성 
[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

[보안 Enclave를 사용한 Always Encrypted](always-encrypted-enclaves.md)는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 보안 Enclave 내에서 바로 데이터베이스 열의 암호화 작업을 수행할 수 있도록 지원합니다. 바로 암호화를 사용하면 암호화 작업을 수행하기 위해 데이터베이스 외부로 데이터를 이동할 필요가 없으므로 더 빠르고 안정적으로 암호화 작업을 수행할 수 있습니다. 

> [!NOTE]
> 바로 암호화가 성능상 이점을 제공하기는 하지만 대형 테이블의 암호화 작업은 시간이 오래 걸리고 상당히 많은 리소스를 사용하므로 그 영향으로 애플리케이션 성능과 가용성이 저하될 수 있습니다.

바로 암호화를 사용하면 [ALTER TABLE ALTER COLUMN(Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) 문을 사용하여 암호화 작업을 트리거할 수도 있습니다. 이 방법은 Enclave 없이는 사용할 수 없습니다.

## <a name="prerequisites"></a>필수 구성 요소
지원되는 암호화 작업과 작업에 사용되는 열 암호화 키에 대한 요구 사항은 다음과 같습니다.
- 일반 텍스트 열 암호화. 열 암호화에 사용되는 열 암호화 키가 Enclave 사용 키여야 합니다.
- 새 암호화 유형 또는/및 새 열 암호화 키를 사용하여 암호화된 열 다시 암호화. 현재 열 암호화 키 및 새 열 암호화 키(현재 키와 다른 경우) 둘 다 Enclave 사용 키여야 합니다.
- 암호화된 열 암호 해독. 열을 보호하는 열 암호화 키가 Enclave 사용 키여야 합니다.

열 암호화 키가 Enclave 사용 키인지 확인하는 방법에 대한 자세한 내용은 [보안 Enclave를 사용한 Always Encrypted 키 관리](always-encrypted-enclaves-manage-keys.md)를 참조하세요.

바로 암호화에는 올바르게 초기화된 보안 Enclave가 있는 SQL Server 인스턴스도 필요합니다. [Always Encrypted 서버 구성 옵션에 대한 Enclave 형식 구성](../../../database-engine/configure-windows/configure-column-encryption-enclave-type.md)을 참조하세요.

암호화 작업을 트리거하는 사용자 또는 애플리케이션은 영향을 받는 열이 포함된 테이블에서 스키마를 변경할 수 있으며 작업에 관련된 열 마스터 키와 데이터베이스의 관련 키 메타데이터에 액세스할 수 있는 권한이 있어야 합니다.

SQL Server Management Studio 또는 사용자 지정 애플리케이션에서 [ALTER TABLE ALTER COLUMN(Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md)을 사용하는 경우에만 바로 암호화를 트리거할 수 있습니다. [Transact-SQL을 사용하여 바로 열 암호화 구성](always-encrypted-enclaves-configure-encryption-tsql.md)을 참조하세요.

> [!NOTE]
> 현재 [Always Encrypted 마법사](always-encrypted-wizard.md) 및 [Set-SqlColumnEncryption](/powershell/module/sqlserver/set-sqlcolumnencryption) cmdlet은 바로 암호화를 지원하지 않으며, 구성이 위의 조건을 충족하는 경우에도 항상 암호화 작업에 대한 데이터를 다운로드합니다. 

## <a name="next-steps"></a>다음 단계
- [Transact-SQL을 사용하여 바로 열 암호화 구성](always-encrypted-enclaves-configure-encryption-tsql.md)
- [Create and use indexes on column using Always Encrypted with secure enclaves](always-encrypted-enclaves-create-use-indexes.md)(보안 Enclave를 사용한 Always Encrypted를 사용하여 열에 인덱스 만들기 및 사용)
- [보안 enclave를 사용한 Always Encrypted를 이용하여 애플리케이션 개발](always-encrypted-enclaves-client-development.md)