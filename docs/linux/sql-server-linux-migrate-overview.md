---
title: "Linux에서 SQL Server로 데이터베이스 마이그레이션 | Microsoft Docs"
description: "이 항목에서는 Linux에서 데이터를 SQL Server 및 데이터베이스 마이그레이션에 대 한 다양 한 옵션을 설명 합니다."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 1619489d-377a-4f32-8930-d4f536539689
ms.custom: H1Hack27Feb2017
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 61b4ba948df071768380d4a6f2b4ddc4421692d8
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="migrate-databases-and-structured-data-to-sql-server-on-linux"></a>Linux에서 SQL Server로 데이터베이스와 구조적된 데이터 마이그레이션 

[!INCLUDE[tsql-appliesto-sslinux-only](../../docs/includes/tsql-appliesto-sslinux-only.md)]

Linux에서 실행 중인 SQL Server 2017 RC2 하 여 데이터베이스와 데이터를 마이그레이션할 수 있습니다. 사용 하도록 선택 하면 원본 데이터 및 특정 시나리오에 따라 다릅니다. 다음 섹션에서는 다양 한 마이그레이션 시나리오에 대 한 유용한 정보를 제공 합니다.

## <a name="migrate-from-sql-server-on-windows"></a>Windows에서 SQL Server에서 마이그레이션
Windows에서 SQL Server 데이터베이스 SQL Server 2017 Linux에서 마이그레이션할 경우 바람직한 방법은 SQL Server 백업 및 복원 사용 것입니다.

1. Windows 컴퓨터의 데이터베이스의 백업을 만듭니다.
2. 대상 SQL Server Linux 컴퓨터에 백업 파일을 전송 합니다.
3. Linux 컴퓨터에서 백업을 복원 합니다. 

마이그레이션하는 방법에 대 한 자습서에 대 한 백업 및 복원으로 데이터베이스는 다음 항목을 참조 합니다.

- [Linux를 Windows에서 SQL Server 데이터베이스를 복원](sql-server-linux-migrate-restore-database.md)합니다.

데이터베이스를 BACPAC 파일로 (프로그램 데이터베이스 스키마 및 데이터를 포함 하는 압축 된 파일)에 내보낼 수 이기도 합니다. BACPAC 파일을 설정한 경우에 Linux 컴퓨터에이 파일을 전송 하 고 후 SQL Server로 가져올 수 있습니다. 자세한 내용은 다음 항목을 참조하세요.

- [내보내기 및 SSMS 또는 SqlPackage.exe를 사용 하 여 데이터베이스 가져오기](sql-server-linux-migrate-ssms.md)

## <a name="migrate-from-other-database-servers"></a>다른 데이터베이스 서버에서 마이그레이션
SQL Server 2017 linux를 다른 데이터베이스 시스템에서 데이터베이스를 마이그레이션할 수 있습니다. 여기에 Microsoft Access, DB2, MySQL, Oracle 및 Sybase 데이터베이스가 포함 됩니다. 이 시나리오에서는 Linux에서 SQL Server로의 마이그레이션을 자동화 하는 SQL Server 관리 Assistant (SSMA)를 사용 합니다. 자세한 내용은 참조 [Linux에서 SQL Server로 데이터베이스 마이그레이션에 사용 하 여 SSMA](sql-server-linux-migrate-ssma.md)합니다.  

## <a name="migrate-structured-data"></a>구조화 된 데이터 마이그레이션
원시 데이터 가져오기에 대 한 기술도 있습니다. 다른 데이터베이스 또는 데이터 원본에서 내보낸 데이터 파일 구조 있을 수 있습니다. 이 경우 bcp 도구 대량 삽입 데이터를 사용할 수 있습니다. 또는 Linux에서 SQL Server 데이터베이스로 데이터를 가져오는 Windows에서 SQL Server Integration Services를 실행할 수 있습니다. SQL Server Integration Services를 사용 하면를 가져오는 동안 데이터에서 더 복잡 한 변환을 실행할 수 있습니다. 

이러한 기술에 대 한 자세한 내용은 다음 항목을 참조 합니다.

- [Bcp 사용 하 여 대량 복사 데이터](sql-server-linux-migrate-bcp.md)
- [추출, 변환 및 SSIS와 Linux에서 SQL Server에 대 한 데이터를 로드 합니다.](sql-server-linux-migrate-ssis.md) 

