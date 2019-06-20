---
title: 원격 테이블 복사본에 대 한 병렬 데이터 웨어하우스 구성 | Microsoft Docs
description: 원격 테이블 복사 기능을 사용 하 여 비 어플라이언스 서버의 SMP SQL Server 데이터베이스에 테이블을 복사 하는 병렬 데이터 웨어하우스를 구성 하는 방법을 설명 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: fdac0b6ed211e223c3fad7ba15ac79a282c61303
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62509525"
---
# <a name="configure-parallel-data-warehouse-for-remote-table-copies"></a>원격 테이블 복사본에 대 한 병렬 데이터 웨어하우스 구성
원격 테이블 복사 기능을 사용 하 여 비 어플라이언스 서버의 SMP SQL Server 데이터베이스에 테이블을 복사 하는 SQL Server PDW 구성 하는 방법에 설명 합니다.  
  
이 항목에서는 원격 테이블 복사본을 구성 하기 위한 구성 단계 중 하나를 설명 합니다. 목록은 모든 구성 단계를 참조 하세요 [원격 테이블 복사](remote-table-copy.md)합니다.  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
원격 테이블 복사본을 사용 하도록 SQL Server PDW를 구성 하려면 다음을 수행 해야 합니다.  
  
-   직접 로그인 하는 기능을 사용 하 여 분석 플랫폼 시스템 관리자 계정이 있어야 합니다  <strong>*appliance_domain*-AD01</strong> 하 고  <strong>*appliance_domain*-AD02</strong> 노드.  
  
-   호스트 이름 또는 대상 서버의 IP 이름을 알고 있어야 합니다.  
  
## <a name="HowToPDW"></a>원격 테이블 복사본에 대 한 SQL Server PDW 구성 합니다. DNS의 호스트 이름을 업데이트 합니다.  
합니다 **CREATE REMOTE TABLE** 원격 테이블 복사본에 사용 되는 문에 SMP Windows 시스템의 IP 이름 또는 IP 주소를 사용 하 여 대상 서버를 지정 합니다. IP 이름을 사용 하려면 DNS 서버에 성공적인 이름 확인에 대 한 항목을 추가 해야 합니다.  
  
다음 단계에는 DNS 서버를 업데이트 하는 방법을 간략하게 설명 합니다.  
  
1.  활성 AD 노드에 로그온 (일반적으로  <strong>*appliance_domain*-AD01</strong>).  
  
2.  DNS 관리자를 엽니다. 아래 **관리 도구** 에 **시작** 메뉴.  
  
3.  DNS 관리자를 사용 하 여 IP 이름을 추가 합니다.  
  
## <a name="see-also"></a>관련 항목  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[DNS 전달자를 사용 하 여 비 어플라이언스 DNS 이름을 확인 하려면](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
<!-- MISSING LINKS 
[Security - Configure Domain Trusts &#40;SQL Server PDW&#41;](../sqlpdw/security-configure-domain-trusts-sql-server-pdw.md)  
-->
  
