---
title: "Scale Out 관리자를 사용하여 SSIS Scale Out 작업자 추가"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ef11448d03bd188aaea425225312af9f681f530c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="add-a-scale-out-worker-with-scale-out-manager"></a>Scale Out 관리자를 사용하여 Scale Out 작업자 추가

Integration Services Scale Out 관리자는 기존 Scale Out 환경에 Scale Out 작업자를 추가하는 복잡성을 대폭 줄입니다. 

아래 단계를 사용하면 Scale Out 토폴로지에 Scale Out 작업자를 추가할 수 있습니다.

## <a name="1-install-scale-out-worker"></a>1. Scale Out 작업자 설치
SQL Server 설치 마법사의 **기능 선택** 페이지에서 Integration Services 및 Scale Out 작업자를 선택합니다. 
![기능 선택 작업자](media/feature-select-worker.PNG)

**Integration Services Scale Out 구성 - 작업자 노드** 페이지에서 "다음"을 클릭하여 여기서 구성하는 과정을 건너뛰고 **Scale Out 관리자**를 사용하여 설치 후 구성을 수행할 수 있습니다.

설치 마법사를 마칩니다.

## <a name="2-open-firewall-on-scale-out-master-computer"></a>2. Scale Out 마스터 컴퓨터에서 방화벽 열기
Scale Out 마스터 컴퓨터에서 Windows 방화벽을 사용하여 Scale Out 마스터 설치 과정에서 지정한 포트(기본적으로 8391) 및 SQL Server 포트(기본적으로 1433)를 엽니다.

## <a name="3-add-scale-out-worker-with-scale-out-manager"></a>3. Scale Out 관리자를 사용하여 Scale Out 작업자 추가
관리자 권한으로 SQL Server Management Studio를 실행하고 Scale Out 마스터의 SQL Server 인스턴스에 연결합니다.

개체 탐색기에서 **SSISDB**를 마우스 오른쪽 단추로 클릭하고 **Scale Out 관리...** 를 선택합니다. 

![Scale Out 관리](media/manage-scale-out.PNG)

나타나는 **Manage Scale 관리**에서 **작업자 관리자**로 전환합니다. "+" 단추를 클릭하고 작업자 연결 대화 상자의 지침을 따릅니다. 자세한 내용은 [Scale Out 관리자](integration-services-ssis-scale-out-manager.md)를 참조하세요.
