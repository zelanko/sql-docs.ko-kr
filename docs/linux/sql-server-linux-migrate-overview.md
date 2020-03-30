---
title: SQL Server on Linux로 데이터베이스 마이그레이션
description: 이 문서에서는 데이터베이스 및 데이터를 SQL Server on Linux로 마이그레이션하는 다양한 옵션을 설명합니다.
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1619489d-377a-4f32-8930-d4f536539689
ms.openlocfilehash: e7affa88f1856571d0b2142f7dcfdf762ed79197
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68129347"
---
# <a name="migrate-databases-and-structured-data-to-sql-server-on-linux"></a>SQL Server on Linux로 데이터베이스 및 정형 데이터 마이그레이션 

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Linux에서 실행되는 SQL Server로 데이터베이스 및 데이터를 마이그레이션할 수 있습니다. 사용할 방법은 원본 데이터 및 특정 시나리오에 따라 달라집니다. 다음 섹션에서는 다양한 마이그레이션 시나리오에 대한 모범 사례를 제공합니다.

## <a name="migrate-from-sql-server-on-windows"></a>Windows의 SQL Server에서 마이그레이션
Windows의 SQL Server 데이터베이스를 SQL Server on Linux로 마이그레이션하려면 SQL Server 백업 및 복원을 사용하는 것이 좋습니다.

1. Windows 머신에서 데이터베이스 백업을 만듭니다.
2. 백업 파일을 대상 SQL Server Linux 머신으로 전송합니다.
3. Linux 머신에서 백업을 복원합니다. 

백업 및 복원을 통해 데이터베이스를 마이그레이션하는 방법에 대한 자습서는 다음 항목을 참조하세요.

- [Windows에서 Linux로 SQL Server 데이터베이스 복원](sql-server-linux-migrate-restore-database.md).

데이터베이스를 BACPAC 파일(데이터베이스 스키마 및 데이터가 포함된 압축 파일)로 내보낼 수도 있습니다. BACPAC 파일이 있는 경우 이 파일을 Linux 머신으로 전송한 후 SQL Server으로 가져올 수 있습니다. 자세한 내용은 아래 항목을 참조하세요.

- [SSMS 또는 SqlPackage.exe를 사용하여 데이터베이스 내보내기 및 가져오기](sql-server-linux-migrate-ssms.md)

## <a name="migrate-from-other-database-servers"></a>다른 데이터베이스 서버에서 마이그레이션
다른 데이터베이스 시스템의 데이터베이스를 SQL Server on Linux로 마이그레이션할 수 있습니다. 여기에는 Microsoft Access, DB2, MySQL, Oracle 및 Sybase 데이터베이스가 포함됩니다. 이 시나리오에서는 SSMA(SQL Server Management Assistant)를 사용하여 SQL Server on Linux로 마이그레이션을 자동화합니다. 자세한 내용은 [SSMA를 사용하여 SQL Server on Linux로 데이터베이스 마이그레이션](sql-server-linux-migrate-ssma.md)을 참조하세요.  

## <a name="migrate-structured-data"></a>정형 데이터 마이그레이션
원시 데이터를 가져오는 기술도 있습니다. 다른 데이터베이스 또는 데이터 원본에서 내보낸 정형 데이터 파일이 있을 수 있습니다. 이 경우 bcp 도구를 사용하여 데이터를 대량 삽입할 수 있습니다. 또는 Windows에서 SQL Server Integration Services를 실행하여 Linux의 SQL Server 데이터베이스로 데이터를 가져올 수 있습니다. SQL Server Integration Services를 사용하면 가져오는 동안 데이터에 대한 더 복잡한 변환을 실행할 수 있습니다. 

이 기술에 대한 자세한 내용은 다음 항목을 참조하세요.

- [bcp를 사용하여 데이터 대량 복사](sql-server-linux-migrate-bcp.md)
- [SSIS를 사용하여 SQL Server on Linux에 대한 데이터 추출, 변환 및 로드](sql-server-linux-migrate-ssis.md) 
