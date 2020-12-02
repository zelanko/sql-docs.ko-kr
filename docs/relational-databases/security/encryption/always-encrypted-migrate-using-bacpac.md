---
description: Always Encrypted를 사용하여 데이터베이스 내보내기 및 가져오기
title: Always Encrypted를 사용하여 데이터베이스 내보내기 및 가져오기 | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3fc54fedce772b267cf19a9396672b61cf6e6254
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127732"
---
# <a name="export-and-import-databases-using-always-encrypted"></a>Always Encrypted를 사용하여 데이터베이스 내보내기 및 가져오기 
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

이 문서에서는[Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)를 사용하여 보호되는 열이 포함된 데이터베이스를 내보내고 가져오는 방법을 설명합니다.

데이터베이스를 내보내는 경우 암호화된 열에 저장된 모든 데이터는 암호화된 형식(암호 텍스트)으로 데이터베이스에서 검색되고 결과 [BACPAC](../../data-tier-applications/data-tier-applications.md)에 배치됩니다. 결과 BACPAC에는 상시 암호화 키에 대한 메타데이터도 포함됩니다.

BACPAC를 데이터베이스로 가져올 때 BACPAC의 암호화된 데이터가 데이터베이스에 로드되고 상시 암호화 키 메타데이터가 다시 생성됩니다. 

원본 데이터베이스(내보낸 데이터베이스)에 저장된 암호화된 열을 쿼리하도록 구성된 애플리케이션이 있는 경우 두 데이터베이스의 키가 동일하기 때문에 애플리케이션이 대상 데이터베이스의 암호화된 데이터를 쿼리할 수 있도록 특별히 수행해야 하는 작업은 없습니다.

데이터베이스를 내보내고 가져오는 방법에 대한 자세한 내용은 다음을 참조하세요.
- [데이터 계층 애플리케이션 내보내기](../../data-tier-applications/export-a-data-tier-application.md)
- [BACPAC 파일을 가져와 새 사용자 데이터베이스 만들기](../../data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database.md)
- [Azure SQL 데이터베이스를 BACPAC 파일로 내보내기](/azure/sql-database/sql-database-export)
- [BACPAC 파일을 Azure SQL Database 데이터베이스로 가져오기](/azure/sql-database/sql-database-import)
- [SqlPackage.exe](../../../tools/sqlpackage.md)

## <a name="permissions-for-migrating-databases-with-encrypted-columns"></a>Encrypted 열을 사용하여 데이터베이스를 마이그레이션할 수 있는 rnjsgks

원본 데이터베이스에 대한 *ALTER ANY COLUMN MASTER KEY* 및 *ALTER ANY COLUMN ENCRYPTION KEY* 권한이 필요합니다. 대상 데이터베이스에 대한 *ALTER ANY COLUMN MASTER KEY*, *ALTER ANY COLUMN ENCRYPTION KEY*, *VIEW ANY COLUMN MASTER KEY DEFINITION* 및 *VIEW ANY COLUMN ENCRYPTION DEFINITION* 권한이 필요합니다.

내보내기 및 가져오기 작업 중에 데이터가 암호화된 상태로 유지되므로 암호화된 열에 구성된 열 마스터 키에 대한 액세스 권한이 필요하지 않습니다.

## <a name="next-steps"></a>다음 단계
- [Always Encrypted를 사용하여 애플리케이션 개발](always-encrypted-client-development.md)

## <a name="see-also"></a>참고 항목
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted를 사용하여 데이터베이스 백업 및 복원](always-encrypted-migrate-using-backup-restore.md)
- [SQL Server 가져오기 및 내보내기 마법사에서 Always Encrypted를 사용하여 열에서 또는 열로 데이터 마이그레이션](always-encrypted-migrate-using-import-export-wizard.md)
- [Always Encrypted를 사용하여 암호화된 데이터를 열에 대량 로드](migrate-sensitive-data-protected-by-always-encrypted.md)