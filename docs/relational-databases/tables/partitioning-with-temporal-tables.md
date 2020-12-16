---
description: 임시 테이블을 사용하여 분할
title: 임시 테이블을 사용하여 분할 | Microsoft 문서
ms.custom: ''
ms.date: 04/26/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 313714b8-4ad1-4c14-93a3-7f628a334a51
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 83180bde505a156c5a6fd5832916e578fb73c52c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484455"
---
# <a name="partitioning-with-temporal-tables"></a>Temporal 테이블을 사용하여 분할


[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]


현재 및 기록 테이블에서 모두 독립적으로 분할을 사용할 수 있습니다. 그러나 분할은 시스템 버전 관리 없이 데이터의 내용을 변경하는 데 사용할 수 없습니다.

> [!NOTE]
> 분할은 서비스 팩 1 이전인 SQL Server 2016 이전 버전에 있는 Enterprise Edition 기능입니다. 분할은 SQL Server 2016 서비스 팩 1 이상 버전의 모든 버전에서 지원됩니다.

- **현재 테이블:**

  - 현재 테이블에 대한 **SWITCH IN** 은 **SYSTEM_VERSIONING** 이 **ON** 인 동안 데이터 로드 및 쿼리를 용이하게 하는 데 사용할 수 있습니다.
  - **SYSTEM_VERSIONING** 이 **SYSTEM_VERSIONING** 이 **ON**

- **기록 테이블:**

  - **SYSTEM_VERSIONING** 이 **ON** 인 동안 기록 테이블에서 **SWITCH OUT** 을 수행하여 더 이상 관련이 없는 기록 데이터 부분을 제거할 수 있습니다.
  - **SWITCH IN** 은 임시 데이터 일관성을 무효화할 수 있으므로 **SYSTEM_VERSIONING** 이 **ON** 인 동안 허용되지 않습니다.

## <a name="next-steps"></a>다음 단계

- [임시 테이블](../../relational-databases/tables/temporal-tables.md)
- [시스템 버전 관리 임시 테이블 시작](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [임시 테이블 시스템 일관성 검사](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [임시 테이블 고려 사항 및 제한 사항](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)
- [임시 테이블 보안](../../relational-databases/tables/temporal-table-security.md)
- [시스템 버전 관리된 임시 테이블에서 기록 데이터의 보존 관리](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [메모리 액세스에 최적화된 테이블을 포함한 시스템 버전 임시 테이블](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [임시 테이블 메타데이터 뷰 및 함수](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
