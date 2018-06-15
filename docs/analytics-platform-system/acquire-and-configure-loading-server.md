---
title: 획득 하 고 로드 서버-병렬 데이터 웨어하우스 구성 | Microsoft Docs
description: 이 문서를 획득 하 고 데이터 로드 병렬 데이터 웨어하우스 (PDW)를 전송 하기 위한 기기 비 Windows 시스템으로 로드 서버를 구성 하는 방법을 설명 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: a796616ad76ba62ea4174cf22c1517c489305055
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31538993"
---
# <a name="acquire-and-configure-a-loading-server-for-parallel-data-warehouse"></a>획득 및 병렬 데이터 웨어하우스에 대 한 로드 서버를 구성 합니다.
이 문서를 획득 하 고 데이터 로드 병렬 데이터 웨어하우스 (PDW)를 전송 하기 위한 기기 비 Windows 시스템으로 로드 서버를 구성 하는 방법을 설명 합니다.  
  
## <a name="Basics"></a>기본 사항  
서버를 로드 합니다.  
  
-   단일 서버 수 있어서는 됩니다. 여러 서버를 로드와 동시에 로드할 수 있습니다.  
  
-   제공 되 고 IT 팀에서 관리 됩니다. PDW에 데이터를 로드 하기 위한 사용할 수 있는 서버로 이미 할 수 있습니다.  
  
-   사용자 고유의 비 어플라이언스 랙에 있으며 분석 플랫폼 시스템 기기 안에 사용할 수 없습니다.  
  
-   Over Ethernet 또는 기기 InfiniBand 네트워크를 통해 어플라이언스에 연결 되어 있습니다. 성능, InfiniBand를 사용 하는 것이 좋습니다.  
  
-   어플라이언스 도메인이 아닌, 사용자의 고객 도메인입니다. 고객 및 어플라이언스 도메인 간의 트러스트 관계가 없습니다.  
  
## <a name="Step1"></a>1 단계: 용량 요구 사항을 결정합니다  
동시 로드를 수행 하는 하나 이상의 로드 서버로 로딩 시스템을 디자인할 수 있습니다. 각 서버를 로드 하는 워크 로드의 성능 및 저장소 요구를 처리할 수 있으므로으로 전용으로 로드 하 고, 필요가 없습니다.  
  
로드 하는 서버에 대 한 시스템 요구 사항 사용자 고유의 작업 부하에 따라 거의 완전히 다릅니다. 사용 하 여는 [서버 용량 계획 워크시트 로드](loading-server-capacity-planning-worksheet.md) 용량 요구 사항을 확인할 수 있습니다.  
  
## <a name="Step2"></a>2 단계:는 sServer 획득  
용량 요구 사항을 더 잘 이해 했으므로 서버 및를 구입 하거나 프로 비전 해야 하는 네트워킹 구성 요소를 계획할 수 있습니다. 다음과 같은 요구 사항 구매 계획에 통합 서버를 구입 하거나 기존 서버를 프로 비전 합니다.  
  
### <a name="R"></a>소프트웨어 요구 사항  
지원되는 운영 체제:  
  
-   Windows Server 2012 또는 Windows Server 2012 r 2입니다. 이러한 운영 체제 FDR 네트워크 어댑터에 필요 합니다.  
  
-   Windows Server 2008 R2. 이 운영 체제에는 DDR 네트워크 어댑터가 필요합니다.  
  
서버는 dwloader 로드 하는 명령줄 도구를 사용 하려면 EN-US 로캘을 사용 해야 합니다. dwloader 다른 로캘을 지원 하지 않습니다.  
  
### <a name="networking-requirements-for-windows-server-2012-and-windows-server-2012-r2"></a>Windows Server 2012 및 Windows Server 2012 r 2에 대 한 요구 사항을 네트워킹  
로드에 대 한 필요 하지는 않지만 InfiniBand 서버를 로드 하는 것에 대 한 권장 되는 연결 종류는입니다. 최상의 성능을 위해 어플라이언스의 InfiniBand 네트워크 로드 서버를 연결 하기 위해 Windows Server 2012 또는 Windows Server 2012 r 2와 FDR InfiniBand 네트워크 어댑터를 사용 합니다.  
  
Windows Server 2012 또는 Windows Server 2012 R2 InfiniBand 연결에 대 한 준비:  
  
1.  서버 랙 하려면 가까이에 어플라이언스에 InfiniBand 전환 어플라이언스에 연결할 수 있도록 합니다. InfiniBand에 대 한 Mellanox 기술에서 자세한 내용은 백서를 참조 [InfiniBand 소개](http://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf)합니다.  
  
2.  단일 또는 이중 포트 Mellanox ConnectX 3 FDR InfiniBand 네트워크 어댑터를 구입 합니다. 데이터 전송 시 네트워크 어댑터 결함 허용을 위해 두 개의 포트를 구입 하는 것이 좋습니다. 두 개의 포트 네트워크 어댑터는 고가용성을 위해 필요 합니다.  
  
3.  이중 포트 카드에 대 한 FDR InfiniBand 케이블 2 개 또는 단일 포트 카드에 대 한 1 FDR InfiniBand 케이블을 구입 합니다. FDR InfiniBand 케이블 어플라이언스의 InfiniBand 네트워크 로드 서버를 연결 합니다. 케이블 길이 사용자 환경에 따라 로드 서버와 어플라이언스 InfiniBand 스위치 간의 거리에 따라 달라 집니다.  
  
## <a name="Step3"></a>3 단계: InfiniBand 네트워크에 서버 연결  
로드 서버 InfiniBand 네트워크를 연결 하려면 다음이 단계를 사용 합니다. 서버 InfiniBand 네트워크를 사용 하지 않는 경우이 단계를 건너뜁니다.  
  
1.  서버 랙 가까이에 어플라이언스에 기기 InfiniBand 네트워크에 연결할 수 있도록 합니다.  
  
2.  서버를 로드에 InfiniBand Mellanox ConnectX 3 FDR InfiniBand 네트워크 어댑터를 설치 합니다.  
  
3.  InfiniBand 네트워크 어댑터를 첫 번째 기기 랙에 두 개의 InfiniBand 스위치 중 하나에 연결 하려면 FDR 케이블을 사용 합니다.  
  
4.  설치 하 고 InfiniBand 네트워크 어댑터에 대 한 적절 한 Windows 드라이버를 구성 합니다.  
  
    -   Windows 용 드라이버 InfiniBand OpenFabrics Alliance 등의 InfiniBand 공급 업체는 업계 consortium에서 개발 됩니다.  올바른 드라이버 InfiniBand 네트워크 어댑터와 함께 배포 될 수 있습니다. 그렇지 않으면 www.openfabrics.org에서 드라이버를 다운로드할 수 있습니다.  
  
5.  네트워크 어댑터에 대 한 InfiniBand 및 DNS 설정을 구성 합니다. 구성 지침은 [구성 InfiniBand 네트워크 어댑터](configure-infiniband-network-adapters.md)합니다.  
  
## <a name="Step4"></a>4 단계: 로드 도구를 설치 합니다.  
클라이언트 도구는 Microsoft 다운로드 센터에서 다운로드할 수 있습니다. 

Dwloader를 설치 하려면 클라이언트 도구에서 dwloader 설치를 실행 합니다.
  
로드에 대 한 Integration Services를 사용 하려는 경우에 Integration Services 및 Integration Services 대상 어댑터를 설치 해야 합니다. 어댑터는 클라이언트 도구에서 사용할 수 있습니다.

<!-- To install the des[Install Integration Services Destination Adapters](install-integration-services-destination-adapters.md). 
--> 
  
## <a name="Step5"></a>5 단계: 로드 시작  
이제 데이터 로드를 시작할 준비가 되었습니다. 참조 항목:  
  
1.  [dwloader 명령줄 로드 도구](dwloader.md)  
  
2.  [부하 개요](load-overview.md)  
  
## <a name="performance"></a>성능  
가장 로드 성능을 Windows Server 2012에서와 같거나 이보다 뒤,에 대 한 데이터를 덮어쓰는 경우 운영 체제 덮어쓰지 것입니다 기존 데이터 0이 되도록 즉시 파일 초기화를 설정 합니다. 인 경우 보안 위험이 이전 데이터 디스크에 여전히 존재 하기 때문에 다음 해야 즉시 파일 초기화를 해제 합니다.  
  
## <a name="Security"></a>보안 알림  
로드할 데이터 어플라이언스에서 저장 되지 않으므로 이후 IT 팀은 로드할 데이터에 대 한 보안의 모든 측면을 관리 하는 일을 담당 합니다. 예를 들어 여기에 로드할 데이터의 보안, 로드, 저장 하는 데 서버 보안 및 SQL Server PDW 어플라이언스에 로드 서버를 연결 하는 네트워킹 인프라의 보안을 관리 합니다.  
  
> [!IMPORTANT]  
> 특히 dwloader 로드 하는 명령줄 도구 사용 하 여 각 로드 서버를 보호 하는 것이 유용 합니다. Dwloader 데이터를 로드할 때 제어 노드를 먼저 인증 있으며 다음 인증을 거친 후 이동 데이터 로드 서버에서 계산 노드에 직접 데이터 채널을 통해. 인증서 유효성 검사는 각 서버를 로드 하 고 각 계산 노드 간 직접 흔들기 하는 동안 발생 하지 않습니다. 이러한 컴퓨터는 계산 노드를 로드 하는 동안 각 데이터 채널에 대 한 잠재적 중간자 개입 공격에 노출 됩니다. 이러한 공격 변조 된 데이터 및/또는 정보 공개 될 수 있습니다.  
  
데이터와 함께 보안 위험을 줄이기 위해 좋습니다 다음:  
  
-   PDW에 데이터를 로드 하는 목적 으로만 사용 되는 한 Windows 계정을 지정 합니다. 부하 위치와 다른 위치에 권한을 보유 하도록이 계정을 사용할 수 있음  
  
-   하나의 PDW 권한을 가진 사용자가 데이터를 로드 하려면를 지정 합니다. 보안 요구 사항에 따라 데이터베이스당 하나의 특정 사용자를 가질 수 있습니다.  
  
-   로드 서버의 작업에 대 한 UNC 경로를 신뢰할 수 있는 내부 네트워크 외부에서 데이터를 끌어오기를 사용할 수 있습니다. 및 공격자가 네트워크에서 또는 이름 확인에 영향을 줄 수 있는 가로채 거 나 SQL Server PDW에 전송 되는 데이터를 수정할 수 있습니다. 변조 및 정보 공개 위험을 표시합니다. 연결에 서명 하도록 요구 하 여 변조를 완화할 수 해야 합니다. 이러한 위험을 완화 하려면 다음 그룹 정책 옵션에서 설정 **보안 설정 \ 로컬 정책 \ 보안 옵션** 로드 서버의: **Microsoft 네트워크 클라이언트: 통신 디지털 서명 (항상): 사용 하도록 설정**  
  
-   Windows Server 2012에서와 같거나 이보다 뒤 즉시 파일 초기화를 해제 합니다. 성능 섹션에 설명 된 대로 성능과 보안 간에입니다. 가장 좋은 보안 요구 사항에 따라 결정 해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
[백업 및 복원 개요](backup-and-restore-overview.md)  
  
