---
title: 원격 테이블 복사
description: 원격 테이블 복사 기능을 사용 하 여 비 어플라이언스 서버에서 SMP SQL Server 데이터베이스에 테이블을 복사 하도록 병렬 데이터 웨어하우스를 구성 하는 방법을 설명 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6c9a0a29b543eb287c7e233d6b1ea77bb2a0d45c
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401261"
---
# <a name="configure-parallel-data-warehouse-for-remote-table-copies"></a>원격 테이블 복사본에 대 한 병렬 데이터 웨어하우스 구성
원격 테이블 복사 기능을 사용 하 여 비 어플라이언스 서버의 SMP SQL Server 데이터베이스에 테이블을 복사 하도록 SQL Server PDW를 구성 하는 방법에 대해 설명 합니다.  
  
이 항목에서는 원격 테이블 복사를 구성 하는 구성 단계 중 하나에 대해 설명 합니다. 모든 구성 단계 목록은 [원격 테이블 복사](remote-table-copy.md)를 참조 하세요.  
  
## <a name="before-you-begin"></a>시작하기 전에  
원격 테이블 복사를 사용 하도록 SQL Server PDW를 구성 하려면 다음을 수행 해야 합니다.  
  
-   <strong> *Appliance_domain*-AD01</strong> <strong> *appliance_domain*및 AD02</strong> 노드에 직접 로그인 할 수 있는 분석 플랫폼 시스템 관리자 계정이 있어야 합니다.  
  
-   대상 서버의 호스트 이름 또는 IP 이름을 파악 합니다.  
  
## <a name="HowToPDW"></a>원격 테이블 복사에 대 한 SQL Server PDW 구성: DNS에서 호스트 이름 업데이트  
원격 테이블 복사에 사용 되는 **CREATE REMOTE table** 문은 SMP Windows 시스템의 ip 주소 또는 ip 이름 중 하나를 사용 하 여 대상 서버를 지정 합니다. IP 이름을 사용 하려면 성공적인 이름 확인을 위해 DNS 서버에 항목을 추가 해야 합니다.  
  
다음 단계에서는 DNS 서버를 업데이트 하는 방법을 간략하게 설명 합니다.  
  
1.  활성 AD 노드에 로그온 합니다 (일반적으로 <strong> *appliance_domain*-AD01</strong>).  
  
2.  DNS 관리자를 엽니다. 이는 **시작** 메뉴의 **관리 도구** 아래에 있습니다.  
  
3.  DNS 관리자를 사용 하 여 IP 이름을 추가 합니다.  
  
## <a name="see-also"></a>참고 항목  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[DNS 전달자를 사용 하 여 비 어플라이언스 DNS 이름 확인](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
<!-- MISSING LINKS 
[Security - Configure Domain Trusts &#40;SQL Server PDW&#41;](../sqlpdw/security-configure-domain-trusts-sql-server-pdw.md)  
-->
  
