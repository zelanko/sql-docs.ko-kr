---
title: "원격 테이블 복사본 (PDW)을 받을 수 외부 SMP SQL Server 구성"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bbd2ed6-064e-4b45-b67b-608dc0f2b2bc
caps.latest.revision: "13"
ms.openlocfilehash: 18b61d60e8ca771feab84b24a9ff53cc7bdfc193
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="configure-an-external-smp-sql-server-to-receive-remote-table-copies"></a>원격 테이블 복사본을 받을 수는 외부 SMP SQL Server 구성
SQL Server PDW에서 원격 테이블 복사본을 받을 수 외부 SQL Server 인스턴스를 구성 하는 방법에 설명 합니다.  
  
이 항목에서는 원격 테이블 복사본을 구성 하기 위한 구성 단계 중 하나. 목록이 모든 구성 단계에 대 한 참조 [원격 테이블 복사](remote-table-copy.md)합니다.  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
외부 SQL Server를 구성 하려면 먼저 다음을 수행 해야 합니다.  
  
-   사용 하는 Windows 시스템 SQL Server 2008 Enterprise Edition 또는 이후 버전을 설치 하거나 이미 설치 되어 준비 합니다. Windows 시스템의 지침에 따라 이미 구성 되어 있어야 [는 외부 Windows 시스템에 수신 원격 테이블 복사본을 사용 하 여 InfiniBand 구성](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)합니다.  
  
-   SQL Server 인스턴스와 Windows 시스템을 구성할 수 있는 Windows 관리자 계정.  
  
-   SQL Server 로그인 계정 (SQL Server가 이미 설치 된 경우) 대상 데이터베이스에 대 한 권한을 부여 하 고 로그인을 만들 수 있는 기능입니다.  
  
## <a name="HowToSQLServer"></a>원격 테이블 복사본을 받을 수는 외부 SMP SQL Server 구성  
원격 테이블 복사 기능은 SQL Server PDW 기기에서 Windows 시스템에서 실행 되는 외부 SMP SQL Server 데이터베이스에 테이블에 복사 합니다. 원격 테이블 복사본을 받을 수 외부 Windows 시스템을 구성한 후 다음 단계를 설치 하 여 Windows 시스템에 SQL Server 구성입니다.  
  
SQL Server를 구성 하려면 다음 단계를 사용 합니다.  
  
1.  Windows 시스템에 SQL Server 2008 Enterprise Edition 또는 이후 버전을 설치 합니다. 이 SMP SQL 서버 라고 합니다.  
  
2.  고정된 TCP 포트에서 TCP/IP 연결을 허용 하도록 SQL Server를 구성 합니다. 이 구성은 기본적으로 비활성화 되어 있으며 SQL Server PDW SMP SQL Server에 연결할 수 있도록 설정 해야 합니다.  
  
3.  Windows 방화벽을 사용 하지 않도록 설정 하거나 Windows 방화벽이 설정 되어 작동할 수 있도록 SMP SQL Server TCP 포트를 구성 하십시오.  
  
4.  SQL Server 인증 모드를 허용 하도록 SQL Server를 구성 합니다. 병렬 데이터 내보내기 항상 인증에 대 한 SQL Server 계정을 사용 합니다.  
  
5.  인증에 사용할 수 있는 SMP SQL Server에서 SQL Server 계정을 확인 합니다. 해당 계정 만들기, 삭제 및 병렬 데이터 내보내기 작업에 대 한 대상 데이터베이스에 있는 테이블 데이터를 삽입할 수 있는 권한을 부여 합니다.  
  
## <a name="BPSQLConfig"></a>원격 테이블 복사본에 대 한 SMP SQL Server 구성에 대 한 모범 사례  
원격 테이블 복사본을 받을 수 SMP SQL Server를 구성할 때 성능을 향상 시키려면 다음 모범 사례를 사용 합니다.  
  
1.  SQL Server 제품 설명서에 설명 된 모범 사례를 따릅니다. 예를 들어, 데이터 암호화를 사용 하도록 설정 합니다. SQL Server 보안 설정에 대 한 자세한 내용은 참조 [Securing SQL Server](../relational-databases/security/securing-sql-server.md) msdn 합니다.  
  
2.  대량 로그 또는 단순 복구 모델을 사용 합니다.  
  
    내보내기 작업은 병렬 데이터 동안, 데이터를 대량으로 새로 만든된 대상 테이블에 삽입 합니다. 대량 삽입 중 최상의 성능을 위해 단순 복구 모델 또는 대량 로그를 사용 하는 대상 데이터베이스를 설정 합니다.  
  
3.  Batch_size 옵션을 사용 하 여 로그 공간을 확보 합니다.  
  
    대량 로그 또는 단순 복구 모델이 사용 하 여 대량 삽입 된 데이터에 대 한 로깅을 최소화 되지만 일부 로깅 여전히 발생 합니다. 로그 파일 증가 단위가 너무 커서를 방지 하려면 정기적으로 로그 공간을 확보 해야 SQL Server batch_size 옵션을 사용 합니다.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
