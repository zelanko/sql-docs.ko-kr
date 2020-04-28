---
title: 원격 테이블 복사본을 받도록 Windows 구성
description: 병렬 데이터 웨어하우스의 원격 테이블 복사 기능과 함께 사용 하기 위해 InfiniBand 네트워크를 사용 하 여 연결 된 비 어플라이언스 Windows 시스템을 구입 및 구성 하는 방법을 설명 합니다. Windows 시스템에서는 SQL Server PDW 데이터베이스에서 원격 테이블 복사본을 수신 하는 SQL Server 데이터베이스를 호스팅합니다. 어플라이언스와 별도로 구입 하 여 어플라이언스 InfiniBand 네트워크에 연결 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 837d41cc929d90b2494682645127f985b5768546
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401310"
---
# <a name="configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband---parallel-data-warehouse"></a>InfiniBand 데이터 웨어하우스를 사용 하 여 원격 테이블 복사본을 받도록 외부 Windows 시스템 구성
SQL Server PDW의 원격 테이블 복사 기능과 함께 사용 하기 위해 InfiniBand 네트워크를 사용 하 여 연결 된 비 어플라이언스 Windows 시스템을 구입 및 구성 하는 방법을 설명 합니다. Windows 시스템에서는 SQL Server PDW 데이터베이스에서 원격 테이블 복사본을 수신 하는 SQL Server 데이터베이스를 호스팅합니다. 어플라이언스와 별도로 구입 하 여 어플라이언스 InfiniBand 네트워크에 연결 합니다.  
  
> [!NOTE]  
> 원격 테이블 복사를 사용 하는 경우 InfiniBand 네트워크를 통한 연결은 필요 하지 않습니다. 이더넷 대역폭이 사용자의 요구를 충족 하는 경우 이더넷 네트워크를 통한 연결을 수행할 수 있습니다.  
  
이 항목에서는 원격 테이블 복사를 구성 하는 구성 단계 중 하나에 대해 설명 합니다. 모든 구성 단계 목록은 [원격 테이블 복사](remote-table-copy.md) 를 참조 하세요.  
  
## <a name="before-you-begin"></a>시작하기 전에  
외부 Windows 시스템을 구성 하기 전에 다음을 수행 해야 합니다.  
  
1.  원격 복사본을 받을 Windows 시스템을 구입 하거나 제공 합니다.  
  
2.  기기 InfiniBand 네트워크에 연결할 수 있도록 컨트롤 랙에 (충분 한 공간이 있는 경우) 또는 어플라이언스에 가까이 가까이 있는 Windows 시스템을 랙 합니다.  
  
3.  어플라이언스 하드웨어 공급 업체에서 InfiniBand 케이블과 InfiniBand 네트워크 어댑터를 구매 합니다. 내보낸 데이터를 받을 때 내결함성을 위해 두 개의 포트를 사용 하 여 네트워크 어댑터를 구매 하는 것이 좋습니다. 두 개의 포트 네트워크 어댑터를 권장 하지만 요구 사항은 아닙니다.  
  
## <a name="configure-an-external-windows-system-to-receive-remote-table-copies"></a><a name="HowToWindows"></a>원격 테이블 복사본을 받도록 외부 Windows 시스템 구성  
외부 Windows 시스템을 구성 하려면 다음 단계를 사용 합니다.  
  
1.  Windows 시스템에 InfiniBand 네트워크 어댑터를 설치 합니다.  
  
2.  InfiniBand 케이블을 사용 하 여 InfiniBand 네트워크 어댑터를 제어 랙의 주 InfiniBand 스위치에 연결 합니다.  
  
3.  InfiniBand 네트워크 어댑터용으로 적절 한 Windows 드라이버를 설치 하 고 구성 합니다.  
  
    Windows 용 InfiniBand 드라이버는 InfiniBand 공급 업체의 업계 컨소시엄의 OpenFabrics 동맹에 의해 개발 되었습니다.  올바른 드라이버가 InfiniBand 어댑터와 함께 배포 되었을 수 있습니다. 그렇지 않은 경우 www.openfabrics.org에서 드라이버를 다운로드할 수 있습니다.  
  
4.  어댑터의 각 포트에 대 한 IP 주소를 구성 합니다. SMP 시스템은이 목적을 위해 예약 된 주소 범위에서 고정 IP 주소를 사용 해야 합니다. 다음 매개 변수에 따라 첫 번째 포트를 구성 합니다.  
  
    -   IP 네트워크 주소: 172.16.132  
  
    -   IP 서브넷 마스크: 255.255.128.0  
  
    -   IP 호스트 범위: 1-254  
  
    두 개의 포트가 있는 InfiniBand 네트워크 어댑터의 경우 다음 매개 변수에 따라 두 번째 포트를 구성 합니다.  
  
    -   IP 네트워크 주소: 172.16.132  
  
    -   IP 서브넷 마스크: 255.255.128.0  
  
    -   IP 호스트 범위: 1-254  
  
5.  두 포트 어댑터를 사용 하거나 여러 외부 Windows 시스템이 어플라이언스에 연결 된 경우 각 IP 서브넷 내에서 각 시스템에 다른 호스트 번호를 할당 합니다.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
