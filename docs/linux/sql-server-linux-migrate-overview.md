---
title: Linux의 SQL Server로 데이터베이스 마이그레이션 | Microsoft Docs
description: 이 문서에서는 Linux의 데이터베이스 마이그레이션 및 SQL Server로 데이터에 대 한 다양 한 옵션을 설명합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.technology: linux
ms.assetid: 1619489d-377a-4f32-8930-d4f536539689
ms.custom: sql-linux
ms.openlocfilehash: 4571589c84d5faaed82ae251a4af262d51e30f3f
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2018
ms.locfileid: "46712881"
---
# <a name="migrate-databases-and-structured-data-to-sql-server-on-linux"></a>Linux의 SQL Server로 데이터베이스 및 구조화 된 데이터 마이그레이션 

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Linux에서 실행 되는 SQL server 데이터베이스 및 데이터를 마이그레이션할 수 있습니다. 사용 하려는 원본 데이터와 특정 시나리오에 따라 다릅니다. 다음 섹션에서는 다양 한 마이그레이션 시나리오에 대 한 모범 사례를 제공합니다.

## <a name="migrate-from-sql-server-on-windows"></a>Windows의 SQL Server에서 마이그레이션
Linux의 SQL Server, Windows의 SQL Server 데이터베이스를 마이그레이션하려는 경우 바람직한 방법은 SQL Server 백업 및 복원 사용 방법은입니다.

1. Windows 컴퓨터에서 데이터베이스의 백업을 만듭니다.
2. 대상 SQL Server Linux 컴퓨터에 백업 파일을 전송 합니다.
3. Linux 컴퓨터의 백업을 복원 합니다. 

백업 및 복원으로 데이터베이스를 마이그레이션하는 방법에 대 한 자습서를 다음 항목을 참조 하세요.

- [Windows에서 Linux에 SQL Server 데이터베이스를 복원](sql-server-linux-migrate-restore-database.md)합니다.

데이터베이스 (데이터베이스 스키마 및 데이터를 포함 하는 압축 된 파일)를 BACPAC 파일로 내보낼 수 이기도 합니다. BACPAC 파일을 사용 하는 경우에 Linux 컴퓨터에이 파일을 전송 하 고 후 SQL Server로 가져올 수 있습니다. 자세한 내용은 다음 항목을 참조하십시오.

- [SSMS 또는 SqlPackage.exe를 사용 하 여 데이터베이스를 내보내고](sql-server-linux-migrate-ssms.md)

## <a name="migrate-from-other-database-servers"></a>다른 데이터베이스 서버에서 마이그레이션
Linux의 SQL Server를 다른 데이터베이스 시스템의 데이터베이스를 마이그레이션할 수 있습니다. 이 Microsoft Access, DB2, MySQL, Oracle 및 Sybase 데이터베이스가 포함 됩니다. 이 시나리오에서는 Linux의 SQL Server로의 마이그레이션을 자동화 하는 SQL Server 관리 Assistant (SSMA)를 사용 합니다. 자세한 내용은 [Linux에서 SQL Server로 데이터베이스 마이그레이션에 사용 하 여 SSMA](sql-server-linux-migrate-ssma.md)합니다.  

## <a name="migrate-structured-data"></a>구조화 된 데이터 마이그레이션
원시 데이터를 가져오기 위한 기술도 있습니다. 다른 데이터베이스 또는 데이터 원본에서 내보낸 데이터 파일을 구조적 있는 수 있습니다. 이 경우 대량 삽입 데이터에 bcp 도구를 사용할 수 있습니다. 또는 Linux에서 SQL Server 데이터베이스로 데이터를 가져오려면 Windows에서 SQL Server Integration Services를 실행할 수 있습니다. SQL Server Integration Services를 사용 하면 가져오는 동안 데이터에 대해 더 복잡 한 변환을 실행할 수 있습니다. 

이러한 기술에 대 한 자세한 내용은 다음 항목을 참조 하세요.

- [Bcp 사용 하 여 데이터 대량 복사](sql-server-linux-migrate-bcp.md)
- [추출, 변환 및 SSIS 사용 하 여 Linux에서 SQL Server에 대 한 데이터를 로드 합니다.](sql-server-linux-migrate-ssis.md) 
