---
title: SQL Server Integration Services Scale Out 관리자 | Microsoft Docs
description: 이 문서에서는 SSIS Scale Out을 관리하는 데 사용할 수 있는 Scale Out 관리자 도구를 설명합니다.
ms.custom: performance
ms.date: 12/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
manager: craigg
ms.openlocfilehash: c384881ffdc02af219de417434d882d41d34c1ef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65718757"
---
# <a name="integration-services-scale-out-manager"></a>Integration Services Scale Out 관리자

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Scale Out 관리자는 하나의 앱으로 전체 SSIS Scale Out 토폴로지를 관리할 수 있는 관리 도구입니다. 여러 컴퓨터에서 관리 작업을 수행하고 Transact-SQL 명령을 실행하는 부담을 없애줍니다.

## <a name="open-scale-out-manager"></a>Scale Out 관리자 열기

Scale Out 관리자를 여는 방법은 두 가지입니다.

### <a name="1-open-scale-out-manager-from-sql-server-management-studio"></a>1. SQL Server Management Studio에서 Scale Out 관리자 열기
SSMS(SQL Server Management Studio)를 열고 Scale Out 마스터의 SQL Server 인스턴스에 연결합니다.

개체 탐색기에서 **SSISDB**를 마우스 오른쪽 단추로 클릭하고 **Scale Out 관리**를 선택합니다.

![Scale Out 관리](media/manage-scale-out.PNG)

> [!NOTE]
> SSMS를 관리자로 실행하는 것이 좋습니다. 일부 Scale Out 관리 작업(예: Scale Out 작업자 추가)에는 관리자 권한이 필요하기 때문입니다.

### <a name="2-open-scale-out-manager-by-running-managementtoolexe"></a>2. ManagementTool.exe를 실행하여 Scale Out 관리자 열기

`%SystemDrive%\Program Files (x86)\Microsoft SQL Server\150\DTS\Binn\Management`에서 `ManagementTool.exe`를 찾습니다. **ManagementTool.exe**를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다. 

Scale Out 관리자가 열리면 Scale Out 마스터의 SQL Server 인스턴스 이름을 입력하고 Scale Out 환경을 관리하도록 연결합니다.

![포털 연결](media/portal-connect-new.png)

## <a name="tasks-available-in-scale-out-manager"></a>Scale Out 관리자에서 가능한 작업
Scale Out 관리자에서는 다음과 같은 작업을 수행할 수 있습니다.

### <a name="enable-scale-out"></a>Scale Out을 사용하도록 설정
SQL Server에 연결한 후 Scale Out이 활성화되어 있지 않으면 **사용**을 선택하여 사용하도록 설정합니다.

![포털 Scale Out을 사용하도록 설정](media/portal-enable-scale-out-new.PNG) 

### <a name="view-scale-out-master-status"></a>Scale Out 마스터 상태 보기
Scale Out 마스터의 상태는 **대시보드** 페이지에 표시됩니다.

![포털 대시보드](media/portal-dashboard-new.PNG)

### <a name="view-scale-out-worker-status"></a>Scale Out 작업자 상태 보기
Scale Out 작업자의 상태는 **작업자 관리자** 페이지에 표시됩니다. 각 작업자를 선택하면 개별 상태를 볼 수 있습니다.

![포털 작업자 관리자](media/portal-worker-manager-new.PNG)

### <a name="add-a-scale-out-worker"></a>Scale Out 작업자 추가
Scale Out 작업자를 추가하려면 Scale Out 작업자 목록의 맨 아래에서 **+** 를 선택합니다. 

추가할 Scale Out 작업자의 컴퓨터 이름을 입력하고 **유효성 검사**를 클릭합니다. Scale Out 관리자는 현재 사용자가 Scale Out 마스터 및 Scale Out 작업자 컴퓨터의 인증서 저장소에 액세스 권한이 있는지 확인합니다.

![작업자 연결](media/connect-worker-new.PNG)

유효성 검사를 성공하면 Scale Out 관리자는 작업자 서버 구성 파일을 읽어서 작업자의 인증서 지문을 가져오려고 시도합니다. 자세한 내용은 [Scale Out 작업자](integration-services-ssis-scale-out-worker.md)를 참조하세요. Scale Out 관리자가 작업자 서비스 구성 파일을 읽을 수 없는 경우 작업자 인증서를 제공할 수 있는 대안이 두 가지 있습니다. 

- 작업자 인증서의 지문을 직접 입력할 수 있습니다.

    ![작업자 인증서 1](media/portal-cert1-new.PNG)

- 아니면 인증서 파일을 제공할 수 있습니다.

    ![작업자 인증서 2](media/portal-cert2-new.PNG)

정보가 수집되면 Scale Out 관리자가 수행할 작업을 설명합니다. 일반적으로 이러한 작업에는 인증서 설치, 작업자 서비스 구성 파일 업데이트 및 작업자 서비스 다시 시작이 포함됩니다.

![포털 추가 확인 1](media/portal-add-confirm1-new.PNG)

작업자 설정에 액세스할 수 없는 경우 수동으로 업데이트하고 작업자 서비스를 다시 시작해야 합니다.

![포털 추가 확인 2](media/portal-add-confirm2-new.PNG)

**확인** 확인란을 선택한 다음 **확인**을 선택하여 Scale Out 작업자 추가를 시작합니다.

### <a name="delete-a-scale-out-worker"></a>Scale Out 작업자 삭제
Scale Out 작업자를 삭제하려면 Scale Out 작업자를 선택한 다음 Scale Out 작업자 목록 맨 아래에서 **-** 를 선택합니다.

### <a name="enable-or-disable-a-scale-out-worker"></a>Scale Out 작업자 사용 또는 사용 안 함
Scale Out 작업자를 사용하거나 사용하지 않으려면 Scale Out 작업자를 선택한 다음 **작업자 사용** 또는 **작업자 사용 안 함**을 선택합니다. 작업자가 오프라인 상태가 아니면 스케일 아웃 관리자에 작업자의 해당 상태가 표시됩니다.

## <a name="edit-a-scale-out-worker-description"></a>Scale Out 작업자 설명 편집
Scale Out 작업자에 대한 설명을 편집하려면 Scale Out 작업자를 선택한 후 **편집**을 선택합니다. 설명 편집을 완료한 후 **저장**을 선택합니다.

![포털 작업자 저장](media/portal-save-worker-new.PNG)

## <a name="next-steps"></a>다음 단계
자세한 내용은 다음 문서를 참조하세요.
-   [Integration Services(SSIS) Scale Out 마스터](integration-services-ssis-scale-out-master.md)
-   [Integration Services(SSIS) Scale Out 작업자](integration-services-ssis-scale-out-worker.md)
