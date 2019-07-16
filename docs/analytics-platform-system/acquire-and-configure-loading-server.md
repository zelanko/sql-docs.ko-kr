---
title: 획득 및 병렬 데이터 웨어하우스 로드 서버-구성 | Microsoft Docs
description: 이 문서에서는 획득 및 병렬 데이터 웨어하우스 (PDW)에 데이터 로드를 제출 하는 것에 대 한 비 어플라이언스 Windows 시스템으로 로드 서버를 구성 하는 방법을 설명 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d753237841695786de3d368bebf9a606875ea634
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961617"
---
# <a name="acquire-and-configure-a-loading-server-for-parallel-data-warehouse"></a>획득 및 병렬 데이터 웨어하우스 로드 서버 구성
이 문서에서는 획득 및 병렬 데이터 웨어하우스 (PDW)에 데이터 로드를 제출 하는 것에 대 한 비 어플라이언스 Windows 시스템으로 로드 서버를 구성 하는 방법을 설명 합니다.  
  
## <a name="Basics"></a>기본 사항  
로드 서버:  
  
-   단일 서버를 사용할 필요가 없습니다 않습니다. 여러 서버를 로드와 동시에 로드할 수 있습니다.  
  
-   제공 되 고 고유한 IT 팀에서 관리 됩니다. 서버 또는 PDW 데이터 로드에 사용할 수 있는 서버를 이미 있을 수 있습니다.  
  
-   사용자 고유의 비 어플라이언스 랙에 있는 및 Analytics Platform System appliance 안에 사용할 수 없습니다.  
  
-   이더넷 또는 어플라이언스 InfiniBand 네트워크를 통해 어플라이언스에 연결 됩니다. 성능을 위해 InfiniBand를 사용 하는 것이 좋습니다.  
  
-   어플라이언스 도메인이 아닌 자신의 고객 도메인입니다. 고객 도메인 및 어플라이언스 도메인 간의 트러스트 관계가 없습니다.  
  
## <a name="Step1"></a>1 단계: 용량 요구 사항 결정  
동시 로드를 수행 하는 하나 이상의 로드 서버로 로드 시스템을 디자인할 수 있습니다. 각 로드 서버 워크 로드의 성능 및 저장소 요구를 처리할 것으로 전용으로 로드 하지 않아도 됩니다.  
  
로드 서버에 대 한 시스템 요구 사항을 고유한 워크 로드에 따라 거의 완전히 달라 집니다. 사용 하 여는 [서버 용량 계획 워크시트 로드](loading-server-capacity-planning-worksheet.md) 용량 요구 사항을 확인할 수 있습니다.  
  
## <a name="Step2"></a>2 단계: sServer 획득  
용량 요구 사항을 이해 했으므로 서버 및을 구입 하거나 프로 비전 해야 하는 네트워킹 구성 요소를 계획할 수 있습니다. 다음과 같은 요구 사항 구매 계획을 통합할 서버를 구입 하거나 기존 서버를 프로 비전 합니다.  
  
### <a name="R"></a>소프트웨어 요구 사항  
지원되는 운영 체제:  
  
-   Windows Server 2012 또는 Windows Server 2012 R2입니다. 이러한 운영 체제 FDR 네트워크 어댑터에 필요 합니다.  
  
-   Windows Server 2008 R2. 이 OS DDR 네트워크 어댑터가 필요합니다.  
  
서버는 dwloader 명령줄 로드 도구를 사용 하려면 EN-US 로캘의 사용 해야 합니다. dwloader 다른 로캘을 지원 하지 않습니다.  
  
### <a name="networking-requirements-for-windows-server-2012-and-windows-server-2012-r2"></a>네트워킹 Windows Server 2012 및 Windows Server 2012 R2에 대 한 요구 사항  
로드 하기 위해 필요 하지는 않지만 InfiniBand는 서버를 로드 하는 것에 대 한 권장 되는 연결 유형입니다. 최상의 성능을 위해 로드 서버 어플라이언스의 InfiniBand 네트워크를 연결 하려면 Windows Server 2012 또는 Windows Server 2012 R2 및 FDR InfiniBand 네트워크 어댑터를 사용 합니다.  
  
Windows Server 2012 또는 Windows Server 2012 R2 InfiniBand 연결을 준비 합니다.  
  
1.  서버 랙 하려면 가까이에 어플라이언스 InfiniBand 전환 어플라이언스에 연결할 수 있도록 합니다. Mellanox 기술에서 대 한 자세한 내용은 InfiniBand 백서를 참조 하세요 [InfiniBand 소개](https://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf)합니다.  
  
2.  단일 또는 이중 포트 Mellanox connectx-3 FDR InfiniBand 네트워크 어댑터를 구입 합니다. 데이터 전송 중 내결함성에 대 한 두 개의 포트를 사용 하 여 네트워크 어댑터를 구입 하는 것이 좋습니다. 두 포트 네트워크 어댑터는 고가용성을 위해 필요 합니다.  
  
3.  이중 포트 카드에 대 한 FDR InfiniBand 케이블 2 개 또는 단일 포트 카드에 대 한 1 FDR InfiniBand 케이블을 구입 합니다. FDR InfiniBand 케이블 어플라이언스의 InfiniBand 네트워크에 로드 서버를 연결 됩니다. 케이블 길이 사용자 환경에 따라 로드 서버와 어플라이언스 InfiniBand 스위치 간의 거리에 따라 달라 집니다.  
  
## <a name="Step3"></a>3 단계: InfiniBand 네트워크에 서버를 연결 합니다.  
로드 서버 InfiniBand 네트워크를 연결 하려면 다음이 단계를 사용 합니다. 서버 InfiniBand 네트워크에 사용 하지 않는 경우이 단계를 건너뜁니다.  
  
1.  어플라이언스 InfiniBand 네트워크에 연결할 수 있도록 서버 랙 어플라이언스로 닫을 합니다.  
  
2.  서버 로드에 InfiniBand Mellanox connectx-3 FDR InfiniBand 네트워크 어댑터를 설치 합니다.  
  
3.  첫 번째 어플라이언스 랙에 두 InfiniBand 스위치 중 하나에 InfiniBand 네트워크 어댑터를 연결할 FDR 케이블을 사용 합니다.  
  
4.  설치 하 고 InfiniBand 네트워크 어댑터에 대 한 적절 한 Windows 드라이버를 구성 합니다.  
  
    -   Windows에 대 한 infiniband InfiniBand 공급 업체의 업계 컨소시엄 OpenFabrics Alliance에서 개발 됩니다.  올바른 드라이버 InfiniBand 네트워크 어댑터를 사용 하 여 배포 될 수 있습니다. 그렇지 않은 경우 www.openfabrics.org 에서 드라이버를 다운로드할 수 있습니다.  
  
5.  네트워크 어댑터에 대 한 InfiniBand 및 DNS 설정을 구성 합니다. 구성 지침을 참조 하세요 [구성 InfiniBand 네트워크 어댑터](configure-infiniband-network-adapters.md)합니다.  
  
## <a name="Step4"></a>4 단계: 로드 도구를 설치 합니다.  
클라이언트 도구는 Microsoft 다운로드 센터에서 다운로드할 수 있습니다. 

Dwloader를 설치 하려면 클라이언트 도구에서 dwloader 설치를 실행 합니다.
  
로드 하기 위해 Integration Services를 사용 하려는 경우 Integration Services 및 Integration Services 대상 어댑터를 설치 해야 합니다. 어댑터는 클라이언트 도구에서 사용할 수 있습니다.

<!-- To install the des[Install Integration Services Destination Adapters](install-integration-services-destination-adapters.md). 
--> 
  
## <a name="Step5"></a>5 단계: 로드를 시작 합니다.  
이제 데이터 로드를 시작할 준비가 되었습니다. 참조 항목:  
  
1.  [dwloader 명령줄 로드 도구](dwloader.md)  
  
2.  [로드 개요](load-overview.md)  
  
## <a name="performance"></a>성능  
최고의 로드 성능은 Windows Server 2012 이상에 대 한 데이터를 덮어쓰는 경우 운영 체제 덮어쓰지 것입니다 기존 데이터 0이 되도록 즉시 파일 초기화를 설정 합니다. 인 경우 보안 위험이 이전 데이터 디스크에 여전히 존재 하기 때문에 다음 해야 인스턴트 파일 초기화를 해제 합니다.  
  
## <a name="Security"></a>보안 알림  
데이터 로드를 어플라이언스에 저장 되지, 않으므로 IT 팀이 로드할 데이터에 대 한 보안의 모든 측면을 관리 하는 일을 담당 합니다. 예를 들어, 로드할 데이터의 보안, 로드, 저장 하는 데 서버의 보안 및 SQL Server PDW 어플라이언스에 로드 서버를 연결 하는 네트워킹 인프라의 보안을 관리 하는 것이 여기 있습니다.  
  
> [!IMPORTANT]  
> 특히 dwloader 명령줄 로드 도구를 사용 하는 각 로드 서버를 보호 하는 것이 반드시 합니다. Dwloader 데이터 로드 되 면 제어 노드에 먼저 인증 한 후 인증에 성공한 후이 이동 데이터 로드 서버에서 계산 노드로 직접 데이터 채널을 통해. 인증서 유효성 검사 중 각 로드 서버와 각 계산 노드 간에 직접 shake 발생 하지 않습니다. 이 로드 하는 동안 각 데이터 채널에 대 한 잠재적인 중간자 개입 공격에 노출 하는 계산 노드를 유지 합니다. 이러한 공격 변조 된 데이터 및/또는 정보가 공개 될 수 있습니다.  
  
데이터를 사용 하 여 보안 위험을 줄이기 위해 다음 찾아보시기:  
  
-   PDW 데이터를 로드 하기 위한 용도로 사용 되는 Windows 계정 하나를 지정 합니다. 로드 위치와 다른 위치에 대 한 권한이이 계정을 허용 합니다.  
  
-   데이터를 로드할 수 있는 권한을 보유 한 PDW 사용자를 지정 합니다. 보안 요구 사항에 따라 데이터베이스 마다 하나의 특정 사용자를 사용할 수 있습니다.  
  
-   로드 서버에서 작업에는 신뢰할 수 있는 내부 네트워크 외부에서 끌어오기 데이터에는 UNC 경로 수락할 수 있습니다. 및 공격자가 네트워크 또는 이름 확인에 영향을 줄 수 있는 기능을 사용 하 여 가로채 거 나 SQL Server PDW에 전송 된 데이터를 수정할 수 있습니다. 이 변조 및 정보 공개 위험을 표시합니다. 연결에 서명 하도록 요구 하 여 변조를 완화할 수 해야 합니다. 이 위험을 완화 하려면에서 다음 그룹 정책 옵션을 설정 **보안 설정 \ 로컬 정책 \ 보안 옵션** 로드 서버에서:  **Microsoft 네트워크 클라이언트: 디지털 서명 통신 (항상): 사용 하도록 설정**  
  
-   Windows Server 2012 이상 인스턴트 파일 초기화를 해제 합니다. 성능 섹션에서 설명 했 듯이이 성능과 보안 간에 균형을 유지 합니다. 보안 요구 사항에 따라 최적의 항목이 결정 해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
[백업 및 복원 개요](backup-and-restore-overview.md)  
  
