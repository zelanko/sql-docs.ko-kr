---
description: Always Encrypted를 사용하여 데이터베이스 백업 및 복원
title: Always Encrypted를 사용하여 데이터베이스 백업 및 복원 | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8b20a6e33c308115c9f8d9b5334ea0ec31035116
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91869043"
---
# <a name="backup-and-restore-databases-using-always-encrypted"></a>Always Encrypted를 사용하여 데이터베이스 백업 및 복원 
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

이 문서에서는 [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)를 사용하여 보호되는 열이 포함된 데이터베이스를 백업 및 복원하는 방법을 설명합니다.

데이터베이스를 백업할 때 생성된 백업 파일에는 암호화된 열에 저장된 암호화와 Always Encrypted 키에 대한 모든 메타데이터가 포함됩니다.

데이터베이스를 복원하면 Always Encrypted 키에 대한 모든 암호화된 데이터와 모든 메타데이터가 복원됩니다. 

다른 서버 또는 다른 이름으로 데이터베이스를 복원하는 경우 두 데이터베이스의 키가 동일하기 때문에 애플리케이션에서 대상 데이터베이스의 암호화된 데이터를 쿼리할 수 있도록 특별한 작업을 수행할 필요가 없습니다.

데이터베이스를 백업 및 복원하는 방법에 대한 자세한 내용은 다음을 참조하세요.
- [Backup Overview (SQL Server)](../../backup-restore/backup-overview-sql-server.md)
- [데이터베이스를 관리되는 인스턴스로 복원](/azure/sql-database/sql-database-managed-instance-get-started-restore)

## <a name="next-steps"></a>다음 단계
- [SQL Server Management Studio로 Always Encrypted를 사용하여 열 쿼리](always-encrypted-query-columns-ssms.md)
- [보안 enclave를 사용한 Always Encrypted를 이용하여 애플리케이션 개발](always-encrypted-enclaves-client-development.md) 

## <a name="see-also"></a>참고 항목
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted를 사용하여 데이터베이스 내보내기 및 가져오기](always-encrypted-migrate-using-bacpac.md)
- [SQL Server 가져오기 및 내보내기 마법사에서 Always Encrypted를 사용하여 열에서 또는 열로 데이터 마이그레이션](always-encrypted-migrate-using-import-export-wizard.md)
- [Always Encrypted를 사용하여 암호화된 데이터를 열에 대량 로드](migrate-sensitive-data-protected-by-always-encrypted.md)