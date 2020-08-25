---
title: 원격 테이블 복사
description: 분석 플랫폼 시스템 병렬 데이터 웨어하우스에서 원격 테이블 복사를 사용 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ecbbdced731e940de46dbde4a65adc486f602c2f
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400487"
---
# <a name="remote-table-copy"></a>원격 테이블 복사
원격 테이블 복사 기능을 사용 하 여 SQL Server PDW 데이터베이스에서 원격 (비 어플라이언스) SMP SQL Server 데이터베이스로 테이블을 복사 하는 방법을 설명 합니다. 원격 테이블 복사를 사용 하 여 SQL Server PDW에 대 한 허브 및 스포크 시나리오를 사용할 수 있습니다.  
  
## <a name="understand-remote-table-copy-for-sql-server-pdw"></a><a name="BasicsPDE"></a>SQL Server PDW에 대 한 원격 테이블 복사 이해  
원격 테이블 복사는 SQL SELECT 문의 결과를 SMP 데이터베이스의 테이블에 복사 하 여 허브 및 스포크 시나리오를 가능 하 게 하는 SQL Server PDW의 기능입니다. 원격 테이블 복사본은 [CREATE REMOTE TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) 문으로 시작 됩니다.  
  
## <a name="requirements-for-using-remote-table-copy"></a><a name="BasicsPrerequisites"></a>원격 테이블 복사 사용을 위한 요구 사항  
이러한 조건이 충족 될 경우 원격 테이블 복사를 사용 하 여 SQL Server PDW에서 SQL Server 데이터베이스로 테이블을 복사할 수 있습니다.  
  
-   대상 데이터베이스는 SQL Server PDW 어플라이언스에 연결할 수 있지만 어플라이언스 내의 서버에 상주 하지 않는 Microsoft Windows® 시스템에서 실행 되는 Microsoft® SQL Server® 인스턴스여야 합니다. 원격 SQL Server InfiniBand 네트워크를 사용 하거나 이더넷 네트워크를 통해 SQL Server PDW에 연결할 수 있습니다.  
  
-   단일 유효한 SQL Server PDW [SELECT](../t-sql/queries/select-transact-sql.md) 문을 사용 하 여 복사할 데이터를 선택할 수 있어야 합니다.  
  
-   대상 서버는 비 어플라이언스 서버여야 합니다. 이 항목의 지침을 사용 하 여 한 어플라이언스에서 다른 어플라이언스로 직접 데이터를 복사할 수 없습니다.  
  
-   대상 서버는 기기의 Infiniband 네트워크에 있는 모든 노드에 액세스할 수 있어야 합니다.  
  
## <a name="configure-remote-table-copy"></a><a name="ConfigureRemote"></a>원격 테이블 복사 구성  
원격 테이블 복사를 사용 하려면 Windows server를 구입 및 구성 하 고, Windows server에서 SQL Server을 구성 하 고 SQL Server PDW을 구성 해야 합니다. 다음 링크를 사용 하 여이 세 가지 구성 단계를 수행 합니다.  
  
1.  [InfiniBand를 사용 하 여 원격 테이블 복사본을 받도록 외부 Windows 시스템 구성](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)  
  
2.  [원격 테이블 복사본을 받도록 외부 SMP SQL Server 구성](configure-an-external-smp-sql-server-to-receive-remote-table-copies.md)  
  
3.  [원격 테이블 복사본에 대 한 SQL Server PDW 구성](configure-sql-server-pdw-for-remote-table-copies.md)  
  
## <a name="perform-a-remote-table-copy"></a><a name="PerformRemote"></a>원격 테이블 복사를 수행 합니다.  
원격 테이블 복사를 수행 하려면 [CREATE REMOTE TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) SQL 문을 사용 합니다. 원격 테이블 만들기 항목에 예가 포함 되어 있습니다.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
