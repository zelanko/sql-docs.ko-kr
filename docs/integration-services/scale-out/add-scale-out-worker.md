---
title: Scale Out 관리자를 사용하여 SSIS Scale Out 작업자 추가
description: 이 문서에서는 Scale Out 관리자를 사용하여 SSIS Scale Out 작업자를 기존 Scale Out 환경에 추가하는 방법을 설명합니다.
ms.custom: performance
ms.date: 12/19/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
manager: craigg
ms.openlocfilehash: 5375f3992cd5d969276b02612f02ab4c32842689
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65718782"
---
# <a name="add-a-scale-out-worker-with-scale-out-manager"></a>Scale Out 관리자를 사용하여 Scale Out 작업자 추가

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Integration Services Scale Out 관리자는 기존 Scale Out 환경에 Scale Out 작업자를 추가하는 프로세스를 간소화합니다. 

다음 단계에 따라 Scale Out 토폴로지에 Scale Out 작업자를 추가하세요.

## <a name="1-install-scale-out-worker"></a>1. Scale Out 작업자 설치
SQL Server 설치 마법사의 **기능 선택** 페이지에서 Integration Services 및 Scale Out 작업자를 선택합니다. 
![기능 선택 작업자](media/feature-select-worker.PNG)

**Integration Services Scale Out 구성 - 작업자 노드** 페이지에서 **다음**을 클릭하여 구성하는 과정을 건너뛰고 **Scale Out 관리자**를 사용하여 설치 후 구성을 수행할 수 있습니다.

설치 마법사를 마칩니다.

## <a name="2-open-the-firewall-on-the-scale-out-master-computer"></a>2. Scale Out 마스터 컴퓨터에서 방화벽 열기
Scale Out 마스터를 설치하는 동안 지정된 포트(기본적으로 8391)와 SQL Server에 대한 포트(기본적으로 1433)를 Scale Out 마스터 컴퓨터의 Windows 방화벽에서 엽니다.

## <a name="3-add-a-scale-out-worker-with-scale-out-manager"></a>3. Scale Out 관리자를 사용하여 Scale Out 작업자 추가
관리자 권한으로 SQL Server Management Studio를 실행하고 Scale Out 마스터의 SQL Server 인스턴스에 연결합니다.

개체 탐색기에서 **SSISDB**를 마우스 오른쪽 단추로 클릭하고 **Scale Out 관리**를 선택합니다. 

![Scale Out 관리](media/manage-scale-out.PNG)

**Scale Out 관리자** 대화 상자에서 **작업자 관리자**로 전환합니다. **+** 를 선택하고 **작업자 연결** 대화 상자의 지침을 따릅니다. 

## <a name="next-steps"></a>다음 단계
자세한 내용은 [Scale Out 관리자](integration-services-ssis-scale-out-manager.md)를 참조하세요.
