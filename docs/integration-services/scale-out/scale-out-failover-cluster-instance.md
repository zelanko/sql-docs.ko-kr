---
title: SQL Server 장애 조치(failover) 클러스터 인스턴스를 통한 고가용성을 위한 Scale Out 지원 | Microsoft Docs
description: 이 문서에서는 SQL Server 장애 조치(failover) 클러스터 인스턴스를 사용하여 고가용성을 위한 SSIS Scale Out을 구성하는 방법을 설명합니다
ms.custom: performance
ms.date: 04/10/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.openlocfilehash: ba171a1ec1082bbcedd77bd5c7bb7a666efd3d04
ms.sourcegitcommit: 6ee40a2411a635daeec83fa473d8a19e5ae64662
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2020
ms.locfileid: "77903800"
---
# <a name="scale-out-support-for-high-availability-via-sql-server-failover-cluster-instance"></a>SQL Server 장애 조치(failover) 클러스터 인스턴스를 통한 고가용성을 위한 Scale Out 지원

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



SQL Server 장애 조치(failover) 클러스터 인스턴스로 Scale Out 마스터 쪽에서 고가용성을 설정하려면 다음을 수행합니다.

## <a name="1-prerequisites"></a>1. 사전 요구 사항
Windows 장애 조치(Failover) 클러스터를 설정합니다. 지침은 [Windows Server 2012용 장애 조치(Failover) 클러스터 기능 및 도구 설치](https://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) 블로그 게시물을 참조하세요. 모든 클러스터 노드에 기능 및 도구를 설치합니다.

## <a name="2-install-sql-server-failover-cluster"></a>2. SQL Server 장애 조치(failover) 클러스터 설치
SQL Server 장애 조치(failover) 클러스터를 설치합니다. 자세한 내용은 [SQL Server 장애 조치(failover) 클러스터 설치](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)를 참조하세요. 설치하는 동안 기능 선택 페이지에서 데이터베이스 엔진 서비스를 선택합니다. 나중에 구성할 수 있도록 SQL Server 네트워크 이름을 기록합니다.

![SQL 네트워크 이름](media/sql-network-name.PNG)

SQL Server 장애 조치(failover) 클러스터에 보조 노드를 추가합니다.

## <a name="3-install-scale-out-master-on-the-primary-node"></a>3. 주 노드에 Scale Out 마스터 설치
클러스터되지 않은 설치를 위한 설치 마법사를 사용하여 주 노드에 Integration Services 및 Scale Out 마스터를 설치합니다. 

설치하는 동안 Scale Out 마스터 인증서의 CN에 SQL Server 네트워크 이름을 포함합니다.

> [!NOTE]
> SSISDB 및 Scale Out 마스터 서비스를 개별적으로 장애 조치(failover)하려면 Scale Out 마스터 구성에 대한 [2. 주 노드에 Scale Out 마스터 설치](scale-out-support-for-high-availability.md#2-install-scale-out-master-on-the-primary-node)를 수행합니다.

## <a name="4-install-scale-out-master-on-the-secondary-node"></a>4. 보조 노드에 Scale Out 마스터 설치
[3. 보조 노드에 Scale Out 마스터 설치](scale-out-support-for-high-availability.md#3-install-scale-out-master-on-the-secondary-node) 수행

## <a name="5-update-the-scale-out-master-service-configuration-file"></a>5. Scale Out 마스터 서비스 구성 파일 업데이트
주 노드와 보조 노드에서 Scale Out 마스터 서비스 구성 파일(\<드라이브\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config)을 업데이트합니다. **SqlServerName**을 기본 인스턴스의 [SQL Server 네트워크 이름]//[인스턴스 이름] 또는 [SQL Server 네트워크 이름]으로 업데이트합니다.

## <a name="6-add-scale-out-master-service-to-sql-server-role-in-windows-failover-cluster"></a>6. Windows 장애 조치(failover) 클러스터에서 SQL Server 역할에 Scale Out 마스터 서비스 추가
장애 조치(Failover) 클러스터 관리자에서 Scale Out용 클러스터에 연결합니다. 탐색기에서 역할을 선택하고, SQL Server 역할을 마우스 오른쪽 단추로 클릭한 다음, 리소스 추가, 일반 서비스를 선택합니다. 

![일반 서비스](media/generic-service.PNG)

새 리소스 마법사에서 Scale Out 마스터 서비스를 선택하고 마법사를 완료합니다. 

Scale Out 마스터 서비스를 온라인 상태로 전환합니다.

![온라인 상태로 전환](media/bring-online.PNG)

> [!NOTE]
> SSISDB 및 Scale Out 마스터 서비스를 개별적으로 장애 조치(failover)하려면 [7. Windows 장애 조치(failover) 클러스터의 Scale Out 마스터 서비스 역할 구성](scale-out-support-for-high-availability.md#7-configure-the-scale-out-master-service-role-of-the-windows-server-failover-cluster)을 수행합니다.

## <a name="7-install-scale-out-workers"></a>7. Scale Out 작업자 설치
작업자 노드에 Scale Out 작업자를 설치합니다. 설치하는 동안 마스터 엔드포인트에 대한 https://[Sql Server 네트워크 이름]:[마스터 포트]를 지정합니다. 

> [!NOTE]
> SSISDB 및 Scale Out 마스터 서비스를 별도로 장애 조치(failover)하려는 경우 Sql Server 네트워크 이름 대신 Scale Out 마스터 서비스 DNS 호스트 이름을 지정합니다.

## <a name="8-install-scale-out-worker-client-certificate"></a>8. Scale Out 작업자 클라이언트 인증서 설치
SQL Server 장애 조치(failover) 클러스터의 모든 노드에 작업자 인증서를 설치합니다. [Scale Out 작업자 클라이언트 인증서 설치](walkthrough-set-up-integration-services-scale-out.md#InstallCert)를 참조하세요.

> [!NOTE]
> Scale Out 관리자는 SQL Server 장애 조치(failover) 클러스터를 지원하지 않습니다. Scale Out 관리자를 사용하여 Scale Out 작업자를 추가하는 경우에도 모든 마스터 노드에 작업자 인증서를 수동으로 설치해야 합니다.

## <a name="next-steps"></a>다음 단계
자세한 내용은 다음 문서를 참조하세요.
-   [Integration Services(SSIS) Scale Out 마스터](integration-services-ssis-scale-out-master.md)
-   [Integration Services(SSIS) Scale Out 작업자](integration-services-ssis-scale-out-worker.md)
