---
title: Stretch Database와 호환 가능한 SQL Server 기능 구성 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c8121ede-1aec-459b-b7b0-1408bb3e62fb
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 03d94268884854c21f5aa6d00eff78a908798a58
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34772739"
---
# <a name="configure-compatible-sql-server-features-with-stretch-database"></a>Stretch Database와 호환 가능한 SQL Server 기능 구성
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


간단한 단계를 수행하여 Stretch Database와 작동하는 다음 SQL Server 기능을 구성합니다.
-   Always On
-   항상 암호화
-   투명한 데이터 암호화
-   임시 테이블

## <a name="configure-always-on-with-stretch-database"></a>Stretch Database를 사용하여 Always On 구성
Always On을 Stretch Database에서 사용하는 경우에는 보조 복제본에서 데이터베이스 마스터 키를 사용할 수 있는지 확인해야 합니다. Stretch Database에서는 원격 Azure 데이터베이스에 연결하기 위해 사용하는 자격 증명을 보호하기 위해 데이터베이스 마스터 키를 사용합니다.

Always On 가용성 그룹을 설정한 후에는 각 보조 복제본에서 저장된 프로시저 **sp_control_dbmasterkey_password** 를 실행하고 Stretch 사용 데이터베이스에 대한 암호를 제공합니다. 자세한 내용과 예제는 [sp_control_dbmasterkey_password](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)를 참조하세요. 

## <a name="configure-always-encrypted-with-stretch-database"></a>Stretch Database를 사용하여 Always Encrypted 구성
Always Encrypted와 Stretch Database를 함께 사용하려면 테이블에서 Stretch Database를 사용하도록 설정하기 전에 선택한 열에서 암호화를 구성해야 합니다.

테이블에서 Stretch Database를 사용하도록 이미 설정한 경우 Always Encrypted 열을 사용하려면 다음을 수행해야 합니다.
1.   테이블에서 Stretch Database를 사용하지 않도록 설정하고 Azure에서 원격 데이터를 다시 가져옵니다. 자세한 내용은 [Stretch Database 비활성화 및 원격 데이터 다시 가져오기](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md)를 사용하세요.
2.   선택된 열에서 Always Encrypted를 구성합니다.
3. 테이블에서 Stretch Database를 다시 사용하도록 설정합니다. 자세한 내용은 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)를 참조하십시오.

## <a name="configure-transparent-data-encryption-tde-with-stretch-database"></a>Stretch Database를 사용하여 TDE(투명한 데이터 암호화) 구성

로컬 데이터베이스에서 TDE를 사용하도록 설정되더라도 Stretch Database 원격 끝점에서는 자동으로 사용 설정되지 않습니다. 데이터베이스에서 Stretch를 사용하도록 설정한 후 원격 끝점에서 TDE를 사용하도록 설정해야 합니다.

## <a name="configure-temporal-tables-with-stretch-database"></a>Stretch Database를 사용하여 temporal 테이블 구성
temporal 테이블을 사용하는 경우에는 현재 테이블이 아닌 기록 테이블에서 Stretch Database를 사용하도록 설정할 수 있습니다.
-   Stretch Database와 temporal 테이블을 사용하는 방법에 대한 지침은 [시스템 버전 관리된 temporal 테이블에서 기록 데이터의 보존 관리](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)를 참조하세요.
-   행을 필터링하고 슬라이딩 윈도우를 사용하여 기록 테이블에서 마이그레이션하려면 [필터 함수를 사용하여 마이그레이션할 행 선택](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)을 참조하세요.
-   테이블이 메모리 액세스에 최적화된 경우 임시 기록 테이블에서 스트레치 데이터베이스를 사용할 수 없습니다. 메모리 액세스에 최적화된 테이블은 지원되지 않습니다.
