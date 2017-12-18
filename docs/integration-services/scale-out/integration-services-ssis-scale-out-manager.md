---
title: "SQL Server Integration Services Scale Out 관리자 | Microsoft Docs"
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
ms.openlocfilehash: 84fe58d4dc7894728c43cb19d17d3444b5b84820
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="integration-services-scale-out-manager"></a>Integration Services Scale Out 관리자

Scale Out 관리자는 단일 위치에서 전체 SSIS Scale Out 토폴로지를 관리할 수 있는 관리 도구입니다. 여러 컴퓨터에서 작업하고 TSQL 명령을 처리해야 하는 부담을 제거합니다. 

Scale Out 관리자를 트리거하는 방법은 두 가지입니다.

## <a name="1-open-scale-out-manager-from-sql-server-management-studio"></a>1. SQL Server Management Studio에서 Scale Out 관리자 열기
SQL Server Management Studio를 열고 Scale Out 마스터의 SQL Server 인스턴스에 연결합니다.

개체 탐색기에서 **SSISDB**를 마우스 오른쪽 단추로 클릭하고 **Scale Out 관리...**를 선택합니다. ![Scale Out 관리](media/manage-scale-out.PNG)

> [!NOTE]
> SQL Server Management Studio는 관리자로 실행하는 것이 좋습니다. "Scale Out 작업자 추가"와 같은 일부 Scale Out 관리 작업에 관리자 권한이 필요하기 때문입니다.


## <a name="2-open-scale-out-manager-by-runing-ismanagerexe-directly"></a>2. ISManager.exe를 직접 실행하여 Scale Out 관리자 열기

ISManager.exe는 %SystemDrive%\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn\Management 아래에 있습니다. **ISManager.exe**를 마우스 오른쪽 단추로 클릭하고 "관리자 권한으로 실행"을 선택합니다. 

창이 열리면 Scale Out 마스터의 SQL Server 이름을 입력하고 SQL Server에 연결해야 Scale Out을 관리할 수 있습니다.

![포털 연결](media/portal-connect.PNG)

Scale Out 관리자에는 아래와 같은 다양한 기능이 제공됩니다. 

## <a name="enable-scale-out"></a>Scale Out을 사용하도록 설정
SQL Server에 연결한 후 Scale Out이 활성화되어 있지 않으면 "사용" 단추를 클릭하여 사용하도록 설정합니다.

![포털 Scale Out을 사용하도록 설정](media/portal-enable-scale-out.PNG) 
## <a name="view-scale-out-master-status"></a>Scale Out 마스터 상태 보기
Scale Out 마스터의 상태는 **대시보드** 페이지에 표시됩니다.

![포털 대시보드](media/portal-dashboard.PNG)
## <a name="view-scale-out-worker-status"></a>Scale Out 작업자 상태 보기
Scale Out 작업자의 상태는 **작업자 관리자** 페이지에 표시됩니다. 각 작업자를 클릭하면 개별 상태를 볼 수 있습니다.

![포털 작업자 관리자](media/portal-worker-manager.PNG)

## <a name="add-scale-out-worker"></a>Scale Out 작업자 추가
Scale Out 작업자를 추가하려면 Scale Out 작업자 목록의 맨 아래에서 "+" 단추를 클릭합니다. 

추가할 Scale Out 작업자의 컴퓨터 이름을 입력하고 "유효성 검사"를 클릭합니다. Scale Out 관리자는 현재 사용자가 Scale Out 마스터 및 Scale Out 작업자의 컴퓨터에 있는 인증서 저장소에 액세스할 수 있는지 확인합니다.

![작업자 연결](media/connect-worker.PNG)

유효성 검사를 통과하면 Scale Out 관리자는 작업자 구성 파일을 읽어서 작업자의 인증서 지문을 가져오려고 합니다. 자세한 내용은 [Scale Out 작업자](integration-services-ssis-scale-out-worker.md)를 참조하세요. 작업자 구성 파일을 읽을 수 없는 경우 작업자 인증서를 제공할 수 있는 대안이 두 가지 있습니다. 

작업자 인증서의 지문을 직접 입력하거나 

![작업자 인증서 1](media/portal-cert1.PNG)

인증서 파일을 제공합니다. 

![작업자 인증서 2](media/portal-cert2.PNG)

모든 정보가 수집되면 Scale Out 관리자에 수행할 작업이 제공됩니다. 일반적으로 인증서 설치, 작업자 구성 파일 업데이트 및 작업자 서비스 다시 시작이 포함됩니다. 

![포털 추가 확인 1](media/portal-add-confirm1.PNG)

작업자 인증서에 액세스할 수 없는 경우 수동으로 직접 업데이트하고 작업자 서비스를 다시 시작해야 합니다.

![포털 추가 확인 2](media/portal-add-confirm2.PNG)

확인 확인란을 클릭하고 Scale Out 작업자를 추가합니다.

## <a name="delete-scale-out-worker"></a>Scale Out 작업자 삭제
Scale Out 작업자를 삭제하려면 Scale Out 작업자를 선택하고 Scale Out 작업자 목록 맨 아래에서 "-" 단추를 클릭합니다.


## <a name="enabledisable-scale-out"></a>Scale Out 설정/해제
Scale Out 작업자를 사용하거나 사용하지 않도록 설정하려면 Scale Out 작업자를 선택하고 "작업자 사용" 또는 "작업자 사용 안 함" 단추를 클릭합니다. 작업자가 오프라인이 아니면 Scale Out 관리자의 작업자 상태가 그에 따라 변경됩니다.

## <a name="edit-scale-out-worker-description"></a>Scale Out 작업자 설명 편집
Scale Out 작업자에 대한 설명을 편집하려면 Scale Out 작업자를 선택하고 "편집" 단추를 클릭합니다. 편집을 마친 후 "저장" 단추를 클릭합니다.

![포털 작업자 저장](media/portal-save-worker.PNG)

