---
title: 가용성 그룹에 대한 클러스터 DTC 서비스
description: 'Always On 가용성 그룹에 대한 Microsoft DTC(Distributed Transaction Coordinator) 서비스를 클러스터링하는 데 필요한 요구 사항 및 단계에 대해 설명합니다. '
ms.custom: seo-lt-2019
ms.date: 08/30/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
ms.assetid: a47c5005-20e3-4880-945c-9f78d311af7a
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 1b5232854920083c685e426e0ca55eeb9a065c70
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726504"
---
# <a name="how-to-cluster-the-dtc-service-for-an-always-on-availability-group"></a>Always On 가용성 그룹에 대한 DTC 서비스를 클러스터링하는 방법

[!INCLUDE[sql windows only](../../../includes/applies-to-version/sql-windows-only.md)]

이 항목에서는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에 대한 Microsoft DTC(Distributed Transaction Coordinator) 서비스를 클러스터링하는 데 필요한 요구 사항 및 단계에 대해 설명합니다. 분산 트랜잭션과 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에 대한 자세한 내용은 [데이터베이스 미러링 또는 Always On 가용성 그룹에 대해 지원되지 않는 데이터베이스 간 트랜잭션(SQL Server)](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)을 참조하세요.

 ## <a name="checklist-preliminary-requirements"></a>검사 목록: 사전 요구 사항

|Task|참조|  
|-----------------|----------|  
|모든 노드, 서비스 및 가용성 그룹이 제대로 구성되었는지 확인합니다.|[Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항(SQL Server)](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)|
|가용성 그룹 DTC 요구 사항이 충족되었는지 확인합니다.|[Always On 가용성 그룹 및 데이터베이스 미러링에 대한 데이터베이스 간 트랜잭션 및 분산 트랜잭션(SQL Server)](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)

## <a name="checklist-clustered-dtc-resource-dependencies"></a>검사 목록: 클러스터형 DTC 리소스 종속성

|Task|참조|  
|-----------------|----------|  
|공유 스토리지 드라이브입니다.|[공유 스토리지 드라이브 구성](https://msdn.microsoft.com/library/cc982358(v=bts.10).aspx). 드라이브 문자 **M**을 사용하는 것이 좋습니다.|
|고유한 DTC 네트워크 이름 리소스입니다.  이름은 Active Directory에서 클러스터 컴퓨터 개체로 등록됩니다.<br /><br />다음 중 하나라도 해당되는지 확인합니다.<br /><br />• DTC 네트워크 이름 리소스를 만드는 사용자에게는 DTC 네트워크 이름 리소스가 상주할 OU 또는 컨테이너에 대한 컴퓨터 만들기 개체 권한이 있습니다.<br /><br />•  사용자에게 컴퓨터 만들기 개체 권한이 없는 경우 도메인 관리자에게 DTC 네트워크 이름 리소스에 대한 클러스터 컴퓨터 개체를 미리 준비하라고 요청합니다.|[Active Directory Domain Services에서 클러스터 컴퓨터 개체 사전 준비](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn466519(v=ws.11))|
|사용 가능한 올바른 고정 IP 주소와, 해당 IP 주소에 대해 적절한 서브넷 마스크입니다.||

## <a name="cluster-the-dtc-resource"></a>DTC 리소스 클러스터
가용성 그룹 리소스를 만든 후 클러스터된 DTC 리소스를 만들어 가용성 그룹에 추가합니다.  샘플 스크립트는 [Always On 가용성 그룹에 대한 클러스터된 DTC 만들기](../../../database-engine/availability-groups/windows/create-clustered-dtc-for-an-always-on-availability-group.md)에 있습니다.


## <a name="checklist-post-clustered-dtc-resource-configurations"></a>검사 목록: 사후 클러스터형 DTC 리소스 구성

|Task|참조|  
|-----------------|----------|  
|클러스터형 DTC 서비스에 대한 네트워크 DTC 액세스를 안전하게 사용하도록 설정합니다.|[MS DTC에 안전하게 네트워크 액세스 사용(영문)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753620(v=ws.10))|
|로컬 DTC 서비스를 중지하고 사용하지 않도록 설정합니다.|[서비스 시작 방법 구성](https://technet.microsoft.com/library/cc755249(v=ws.11).aspx)|
|가용성 그룹의 각 인스턴스에 대해 SQL Server 서비스를 순환합니다.  필요에 따라 가용성 그룹을 장애 조치(Failover)합니다.|[가용성 그룹의 계획된 수동 장애 조치(Failover) 수행(SQL Server)](../../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)<br /><br />[데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스 시작, 중지, 일시 중지, 재개 및 다시 시작](../../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)|

- 서버가 Windows Server 2012 R2인 경우 운영 체제에 [KB 3030373](https://support.microsoft.com/kb/3090973) 이 적용되어 있어야 합니다.

- [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)의 검사 목록에 따라 가용성 그룹에 대해 서버를 준비합니다.

- [**Always On 가용성 그룹**](../../../database-engine/availability-groups/windows/configuration-of-a-server-instance-for-always-on-availability-groups-sql-server.md)에 대해 서버 인스턴스를 구성합니다.

### <a name="resources"></a>리소스


[가용성 그룹에서 DTC 테스트에 대한 추가 정보(영문)](/archive/blogs/dataplatform/sql-server-2016-dtc-support-in-availability-groups)

[Always On 가용성 그룹 시스템 뷰 모니터링](monitor-availability-groups-transact-sql.md)

[가용성 그룹 단계별 만들기](create-an-availability-group-transact-sql.md)


[가용성 그룹의 SQL Server 2016 DTC 지원(영문)](/archive/blogs/dataplatform/sql-server-2016-dtc-support-in-availability-groups) 

[외부 링크: Windows Server 2008 R2를 사용하여 SQL Server의 클러스터된 인스턴스에 대한 DTC 구성](https://sqlha.com/2013/03/12/how-to-properly-configure-dtc-for-clustered-instances-of-sql-server-with-windows-server-2008-r2/)