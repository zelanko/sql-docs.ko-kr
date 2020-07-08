---
title: SQL Server 가져오기 및 내보내기 마법사로 Always Encrypted를 사용하여 열 간에 데이터 마이그레이션 | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL13.SWB.COLUMNMASTERKEY.PAGE.F1
- SQL13.SWB.COLUMNENCRYPTIONKEY.PAGE.F1
- SQL13.SWB.COLUMNMASTERKEY.ROTATION.F1
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 42898b255427c5f3d870a21e17e2cdeb17039919
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85627322"
---
# <a name="migrate-data-to-or-from-columns-using-always-encrypted-with-sql-server-import-and-export-wizard"></a>SQL Server 가져오기 및 내보내기 마법사로 Always Encrypted를 사용하여 열 간에 데이터 마이그레이션 
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

[SQL Server 가져오기 및 내보내기 마법사](../../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)는 원본에서 대상으로 데이터를 복사할 수 있는 도구입니다. 이 문서에서는 원본 및/또는 대상이 [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)로 보호된 열을 포함하는 SQL Server 데이터베이스일 경우 SQL Server 가져오기 및 내보내기 마법사를 사용하는 방법을 설명합니다.

## <a name="migration-scenarios"></a>마이그레이션 시나리오
SQL Server 가져오기 및 내보내기 마법사를 사용하여 암호화된 열로 또는 암호화된 열에서 데이터를 마이그레이션하는 다음과 같은 시나리오를 구현할 수 있습니다.

### <a name="encrypt-plaintext-data-on-migration"></a>마이그레이션 시 일반 텍스트 데이터 암호화
데이터 원본에 일반 텍스트 데이터가 포함되어 있고 대상이 암호화된 열을 포함하는 SQL Server 데이터베이스인 경우 SQL Server 가져오기 및 내보내기 마법사를 사용하여 원본에서 일반 텍스트 데이터를 검색하고 암호화한 다음 암호화된 데이터(암호 텍스트)를 대상 데이터베이스의 암호화된 열에 복사할 수 있습니다. 이 마이그레이션 시나리오에서 데이터 원본은 SQL Server 가져오기 및 내보내기 마법사에서 지 원하는 모든 데이터 저장소일 수 있습니다. 예를 들어 파일, SQL Server 데이터베이스 또는 다른 데이터베이스 시스템의 데이터베이스입니다.

SQL Server 가져오기 및 내보내기 마법사에서 데이터를 암호화할 수 있게 하려면 대상 데이터베이스 연결에 Always Encrypted를 사용하도록 설정해야 하며 대상 데이터베이스 열에서 데이터를 보호하는 키에 대한 액세스 권한이 있어야 합니다. 자세한 내용은 [데이터베이스 연결에 Always Encrypted 사용 및 사용 안 함](#enable-and-disable-always-encrypted-for-a-database-connection) 및 [마이그레이션 중 데이터 암호화 또는 암호 해독 권한](#permissions-for-encrypting-or-decrypting-data-during-migration)을 참조하세요.

### <a name="decrypt-encrypted-data-on-migration"></a>마이그레이션 시 암호화된 데이터 암호 해독
SQL Server 데이터베이스의 암호화된 데이터베이스 열에 저장된 데이터를 마이그레이션하는 경우 SQL Server 가져오기 및 내보내기 마법사가 데이터의 암호를 해독하고 해독된(일반 텍스트) 데이터를 대상에 복사하도록 구성할 수 있습니다. 이 대상은 SQL Server 가져오기 및 내보내기 마법사에서 지원하는 모든 데이터 저장소 일 수 있습니다(예: 파일, SQL Server 데이터베이스 또는 다른 데이터베이스 시스템의 데이터베이스).

SQL Server 가져오기 및 내보내기 마법사에서 데이터의 암호를 해독할 수 있게 하려면 원본 데이터베이스 연결에 Always Encrypted를 사용하도록 설정해야 하며 원본 데이터베이스 열에서 데이터를 보호하는 키에 대한 액세스 권한이 있어야 합니다. 자세한 내용은 [데이터베이스 연결에 Always Encrypted 사용 및 사용 안 함](#enable-and-disable-always-encrypted-for-a-database-connection) 및 [마이그레이션 중 데이터 암호화 또는 암호 해독 권한](#permissions-for-encrypting-or-decrypting-data-during-migration)을 참조하세요.

### <a name="re-encrypt-data-on-migration"></a>마이그레이션 시 데이터 다시 암호화
원본 SQL Server 데이터베이스의 암호화된 열에서 같거나 다른 SQL Server 데이터베이스의 암호화된 열로 데이터를 복사하는 경우 SQL Server 가져오기 및 내보내기 마법사가 원본에서 데이터를 검색하여 데이터의 암호를 해독하고 대상 데이터베이스의 암호화된 열에 삽입하기 전에 다시 암호화하도록 구성할 수 있습니다. 대상 열의 스키마(예: 열 데이터 형식, 암호화 유형 및 열 암호화 키)가 원본 열의 스키마와 다른 경우 이 방법을 사용합니다.

SQL Server 가져오기 및 내보내기 마법사에서 데이터를 암호화하고 암호 해독할 수 있게 하려면 원본 데이터베이스 연결 및 대상 데이터베이스 연결 모두에 Always Encrypted를 사용하도록 설정해야 하며 원본 및 대상 데이터베이스 열 모두에서 데이터를 보호하는 키에 대한 액세스 권한이 있어야 합니다. 자세한 내용은 [데이터베이스 연결에 Always Encrypted 사용 및 사용 안 함](#enable-and-disable-always-encrypted-for-a-database-connection) 및 [마이그레이션 중 데이터 암호화 또는 암호 해독 권한](#permissions-for-encrypting-or-decrypting-data-during-migration)을 참조하세요.

### <a name="keep-data-encrypted-during-migration"></a>마이그레이션 중 데이터를 암호화 상태로 유지
원본 SQL Server 데이터베이스의 암호화된 열에서 같거나 다른 SQL Server 데이터베이스의 암호화된 열로 데이터를 복사하고 대상 열이 원본 열과 **정확히** 동일한 스키마(동일한 데이터 형식, 암호화 유형, 열 암호화 키 등)를 사용하는 경우 SQL Server 가져오기 및 내보내기 마법사가 원본 열에서 암호 텍스트를 검색하여 대상 SQL Server 데이터베이스의 암호화된 열에 암호화된 데이터(암호 텍스트)를 삽입하도록 구성할 수 있습니다. 

이 시나리오에서는 SQL Server를 지원하는 모든 데이터 공급자를 사용하여 원본 또는 대상 SQL Server 데이터베이스에 연결할 수 있습니다. Always Encrypted를 지원하는 공급자를 사용하여 대상 데이터베이스에 연결하는 경우 데이터베이스 연결에 Always Encrypted를 사용하지 않도록 설정되었는지 확인해야 합니다. 자세한 내용은 [데이터베이스 연결에 Always Encrypted 사용 및 사용 안 함](#enable-and-disable-always-encrypted-for-a-database-connection)을 참조하세요.

또한 SQL Server 가져오기 및 내보내기 마법사가 대상 데이터베이스에 연결하는 데 사용하는 데이터베이스 보안 주체(사용자)가 `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` 옵션을 `ON`으로 설정하여 구성되었는지 확인해야 합니다. 이 옵션은 대량 복사 작업에서 서버에 대한 암호화 메타데이터 검사를 수행하지 않습니다. 이 옵션을 사용하면 마법사가 데이터의 암호를 해독하지 않고 암호화된 데이터를 대상 데이터베이스에 대량 삽입할 수 있습니다. 자세한 내용은 [Always Encrypted로 보호되는 열에 암호화된 데이터 대량 로드](migrate-sensitive-data-protected-by-always-encrypted.md)를 참조하세요.

## <a name="enable-and-disable-always-encrypted-for-a-database-connection"></a>데이터베이스 연결에 Always Encrypted 사용 및 사용 안 함
마이그레이션 시나리오에서 SQL Server 가져오기 및 내보내기 마법사가 데이터를 암호화 및/또는 암호 해독할 수 있어야 하는 경우에는 Always Encrypted를 지원하는 데이터 공급자를 사용하여 원본 SQL Server 데이터베이스 연결 및/또는 대상 SQL Server 데이터베이스 연결을 구성해야 합니다. 또한 원본 및/또는 대상 데이터베이스 연결에 Always Encrypted를 사용하도록 설정해야 합니다.

마법사가 해당 연결에서 데이터를 암호화 또는 암호 해독하지 않아도 되는 경우 연결에 모든 데이터 공급자를 사용할 수 있습니다.

SQL Server 가져오기 및 내보내기 마법사의 다음 데이터 공급자는 Always Encrypted를 지원합니다.

- .NET Framework Data Provider for SQL Server
  - 마법사가 실행되는 컴퓨터가 .NET Framework 4.6.1 이상을 사용해야 합니다.
  - 연결에 Always Encrypted을 사용하도록 설정하려면 연결 속성에서 `Column Encryption Setting`을 `Enabled`로 설정합니다. Always Encrypted를 사용하지 않도록 설정하려면 `Column Encryption Setting`을 `Disabled`로 설정합니다. 자세한 내용은 [.NET Framework Data Provider for SQL Server를 사용하여 SQL Server에 연결](../../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md#connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server) 및 [애플리케이션 쿼리에 대해 Always Encrypted 사용](develop-using-always-encrypted-with-net-framework-data-provider.md#enabling-always-encrypted-for-application-queries)을 참조하세요.
- .NET Framework Data Provider for ODBC
  - Microsoft ODBC Driver 13.1 이상 버전을 설치합니다.
    - 연결에 Always Encrypted을 사용하도록 설정하려면 연결 속성에서 `Column Encryption`을 `Enabled`로 설정합니다. Always Encrypted를 사용하지 않도록 설정하려면 `Column Encryption`을 `Disabled`로 설정합니다. 자세한 내용은 [ODBC Driver for SQL Server를 사용하여 SQL Server에 연결](../../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md#connect-to-sql-server-with-the-odbc-driver-for-sql-server) 및 [ODBC 애플리케이션에 대해 Always Encrypted 사용](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#enabling-always-encrypted-in-an-odbc-application)을 참조하세요.

## <a name="permissions-for-encrypting-or-decrypting-data-during-migration"></a>마이그레이션 중 데이터 암호화 또는 암호 해독 권한

SQL Server 원본 또는 대상에 저장된 데이터를 암호화 또는 암호 해독하려면 원본 데이터베이스에서 *VIEW ANY COLUMN MASTER KEY DEFINITION* 및 *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* 권한이 있어야 합니다.

또한 암호화하거나 암호를 해독할 데이터를 저장하는 열에 대해 구성된 열 마스터 키에 액세스할 수 있어야 합니다.

- **인증서 저장소 - 로컬 컴퓨터** - 열 마스터 키로 사용되는 인증서에 대한 읽기 권한이 있거나 컴퓨터의 관리자여야 합니다.
- **Azure Key Vault** - 열 마스터 키를 포함하는 자격 증명 모음에 대한 _get_, _unwrapKey_ 및 _verify_ 권한이 필요합니다.
- **CNG(키 저장소 공급자)** – 저장소 및 KSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.
- **CAPI(암호화 서비스 공급자)** – 저장소 및 CSP 구성에 따라 키 저장소 또는 키를 사용할 때 필수 권한 및 자격 증명을 확인하는 메시지가 표시될 수도 있습니다.
자세한 내용은 [열 마스터 키 만들기 및 저장(상시 암호화)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계
- [SQL Server Management Studio로 Always Encrypted를 사용하여 열 쿼리](always-encrypted-query-columns-ssms.md)
- [Always Encrypted를 사용하여 애플리케이션 개발](always-encrypted-client-development.md)

## <a name="see-also"></a>참고 항목
- [Always Encrypted](always-encrypted-database-engine.md)
- [Always Encrypted를 사용하여 데이터베이스 내보내기 및 가져오기](always-encrypted-migrate-using-bacpac.md)
- [Always Encrypted를 사용하여 데이터베이스 백업 및 복원](always-encrypted-migrate-using-backup-restore.md)
- [Always Encrypted를 사용하여 암호화된 데이터를 열에 대량 로드](migrate-sensitive-data-protected-by-always-encrypted.md)