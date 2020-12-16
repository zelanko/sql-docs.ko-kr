---
title: SSMS를 사용하여 상시 암호화 구성
description: SSMS(SQL Server Management Studio)를 사용하여 Always Encrypted 데이터베이스를 구성하고 관리하는 작업을 설명합니다.
ms.custom: seo-lt-2019
ms.date: 10/31/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d3d018e1cd1230e50702192ebc675fd2ed1b155f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97459989"
---
# <a name="configure-always-encrypted-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 상시 암호화 구성
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

이 문서에서는 [SSMS(SQL Server Management Studio)](../../../ssms/download-sql-server-management-studio-ssms.md)를 사용하여 상시 암호화를 구성하고 상시 암호화를 사용하는 데이터베이스를 관리하는 작업에 대해 설명합니다.

## <a name="security-considerations-when-using-ssms-to-configure-always-encrypted"></a>SSMS를 사용하여 Always Encrypted를 구성할 때의 보안 고려 사항

SSMS를 사용하여 상시 암호화를 구성하는 경우 SSMS에서 상시 암호화 키와 중요한 데이터를 둘 다 처리하므로 키와 데이터가 SSMS 프로세스 내에서 일반 텍스트로 모두 표시됩니다. 따라서 보안 컴퓨터에서 SSMS를 실행하는 것이 중요합니다. 데이터베이스가 SQL Server에서 호스트된 경우 SQL Server 인스턴스를 호스트하는 컴퓨터 이외의 다른 컴퓨터에서 SSMS를 실행합니다. 상시 암호화의 주요 목표는 데이터베이스 시스템이 손상된 경우에도 암호화된 중요한 데이터를 안전하게 보호하는 것이므로 SQL Server 컴퓨터에서 키 또는 중요한 데이터를 처리하는 PowerShell 스크립트를 실행하면 기능의 이점이 감소하거나 무효화될 수 있습니다. 추가 권장 사항을 보려면 [키 관리에 대한 보안 고려 사항](overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management)을 참조하세요.

SSMS는 데이터베이스를 관리하는 사용자(DBA)와 암호화 암호를 관리하고 일반 텍스트 데이터에 액세스할 수 있는 사용자(보안 관리자 및/또는 애플리케이션 관리자) 간의 역할 구분을 지원하지 않습니다. 조직에서 역할 구분을 적용하는 경우 PowerShell을 사용하여 상시 암호화를 구성해야 합니다. 자세한 내용은 [Always Encrypted를 위한 키 관리 개요](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md) 및 [PowerShell을 사용하여 상시 암호화 구성](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)을 참조하세요. 

## <a name="always-encrypted-tasks-using-ssms"></a>SSMS를 사용하는 Always Encrypted 작업

- [SQL Server Management Studio를 사용하여 Always Encrypted 키 프로비전](configure-always-encrypted-keys-using-ssms.md)
- [SQL Server Management Studio를 사용하여 Always Encrypted 키 회전](rotate-always-encrypted-keys-using-ssms.md)
- [Always Encrypted 마법사를 사용하여 열 암호화 구성](always-encrypted-wizard.md)
- [DAC 패키지로 Always Encrypted를 사용하여 열 암호화 구성](configure-always-encrypted-using-dacpac.md)
- [SQL Server Management Studio로 Always Encrypted를 사용하여 열 쿼리](always-encrypted-query-columns-ssms.md)
- [Always Encrypted를 사용하여 데이터베이스 내보내기 및 가져오기](always-encrypted-migrate-using-bacpac.md)
- [Always Encrypted를 사용하여 데이터베이스 백업 및 복원](always-encrypted-migrate-using-backup-restore.md)
- [SQL Server 가져오기 및 내보내기 마법사에서 Always Encrypted를 사용하여 열에서 또는 열로 데이터 마이그레이션](always-encrypted-migrate-using-import-export-wizard.md)

## <a name="see-also"></a>참고 항목
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted를 위한 키 관리 개요](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [PowerShell을 사용하여 Always Encrypted 구성](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)
- [Always Encrypted를 사용하여 애플리케이션 개발](always-encrypted-client-development.md)
