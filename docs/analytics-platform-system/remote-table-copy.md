---
title: 원격 테이블 복사-병렬 데이터 웨어하우스 | Microsoft Docs
description: 원격 테이블 복사본을 사용 하 여 분석 플랫폼 시스템 병렬 데이터 웨어하우스에서 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5ed517a471368e4192ad7393a92274424d37f975
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
---
# <a name="remote-table-copy"></a>원격 테이블 복사
원격 (비 어플라이언스) SMP SQL Server 데이터베이스에 SQL Server PDW 데이터베이스에서 테이블을 복사 하려면 원격 테이블 복사 기능을 사용 하는 방법을 설명 합니다. SQL Server PDW에 대 한 허브 및 스포크 시나리오를 사용 하도록 설정 하려면 원격 테이블 복사본을 사용 합니다.  
  
## <a name="BasicsPDE"></a>SQL Server PDW에 대 한 원격 테이블 복사본 이해  
원격 테이블 복사는 SMP 데이터베이스의 테이블에는 SQL SELECT 문의 결과 복사 하 여 허브 및 스포크 시나리오를 사용 하는 SQL Server PDW의 기능입니다. 원격 테이블 복사본으로 시작 되는 [CREATE 원격 TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) 문.  
  
## <a name="BasicsPrerequisites"></a>원격 테이블 복사본을 사용 하기 위한 요구 사항  
이러한 조건이 충족 되 면 SQL Server 데이터베이스에 SQL Server PDW에서 원격 테이블 복사본에 테이블을 사용할 수 있습니다.  
  
-   대상 데이터베이스를 SQL Server PDW 어플라이언스에 연결할 수 있지만 어플라이언스에 내에서 서버에 상주 하지 않는 Microsoft Windows® 시스템에서 실행 되는 Microsoft® SQL Server®의 인스턴스여야 합니다. 원격 SQL Server 이더넷 네트워크를 통해 또는 InfiniBand 네트워크를 사용 하 여 SQL Server PDW에 연결할 수 있습니다.  
  
-   데이터를 복사 단일 유효한 SQL Server PDW를 사용 하 여 선택할 수 있어야 합니다 [선택](../t-sql/queries/select-transact-sql.md) 문.  
  
-   대상 서버는 비 어플라이언스 서버여야 합니다. 이 항목의 지시를 사용 하 여 다른 하 한 기기에서 직접 데이터를 복사할 수 없습니다.  
  
-   대상 서버는 어플라이언스의 Infiniband 네트워크에서 모든 노드에 액세스할 수 있어야 합니다.  
  
## <a name="ConfigureRemote"></a>원격 테이블 복사본을 구성 합니다.  
원격 테이블 복사본을 사용 하려면 필요한 구입 하 고 Windows server를 구성 합니다. Windows server에서 SQL Server를 구성 했으며 SQL Server PDW 구성 다음 링크를 사용 하 여 이러한 세 개의 구성 단계를 수행 합니다.  
  
1.  [InfiniBand를 사용 하 여 원격 테이블 복사본을 받을 수는 외부 Windows 시스템 구성](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)  
  
2.  [원격 테이블 복사본을 받을 수는 외부 SMP SQL Server 구성](configure-an-external-smp-sql-server-to-receive-remote-table-copies.md)  
  
3.  [원격 테이블 복사본에 대 한 SQL Server PDW 구성](configure-sql-server-pdw-for-remote-table-copies.md)  
  
## <a name="PerformRemote"></a>원격 테이블 복사를 수행 합니다.  
원격 테이블 복사본을 수행 하려면는 [CREATE 원격 TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) SQL 문입니다. 예로 CREATE REMOTE TABLE 항목에 포함 되어 있습니다.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
