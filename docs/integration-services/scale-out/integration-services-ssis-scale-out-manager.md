---
title: "SQL Server Integration Services 관리자 확장 | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 96748296acd1b2f5ba98558335fece9637eadb87
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-scale-out-manager"></a>Integration Services 확장 관리자

스케일 아웃 관리자는 단일 위치에서 전체 SSIS 스케일 아웃 토폴로지를 관리할 수 있는 관리 도구입니다. 여러 컴퓨터에서 작동 하 고 TSQL 명령으로 처리 해야 하는 부담을 제거 합니다. 

두 가지 방법으로 관리자 스케일 아웃을 트리거할 수 있습니다.

## <a name="1-open-scale-out-manager-from-sql-server-management-studio"></a>1. SQL Server Management Studio에서 확장 관리자를 열려면
SQL Server Management Studio를 열고 스케일 아웃 마스터의 SQL Server 인스턴스에 연결 합니다.

마우스 오른쪽 단추로 클릭 **SSISDB** 고 개체 탐색기에서 **스케일 아웃 관리...** . 
![확장 관리](media/manage-scale-out.PNG)

> [!NOTE]
> 범위 확장 관리 작업 "작업자 확장 추가" 하는 등의 일부으로 관리자 권한으로 SQL Server Management Studio를 실행 하려면 관리자 권한이 필요 합니다 것이 좋습니다.


## <a name="2-open-scale-out-manager-by-runing-ismanagerexe-directly"></a>2. 직접 ISManager.exe 실행 하 여 스케일 아웃 관리자를 열려면

ISManager.exe는 %SystemDrive%\Program 파일 (x86) \Microsoft SQL Server\140\DTS\Binn\Management에서 찾습니다. 마우스 오른쪽 단추로 클릭 **ISManager.exe** 고 "관리자 권한으로 실행"을 선택 합니다. 

서비스가 열리는 후 스케일 아웃 마스터의 Sql Server 이름을 입력 하 고 관리 하면 스케일 아웃 하기 전에 연결 해야 합니다.

![포털 연결](media/portal-connect.PNG)

스케일 아웃 관리자는 아래와 같이 다양 한 기능을 제공합니다. 

## <a name="enable-scale-out"></a>확장을 사용 하도록 설정
범위 확장을 사용 하지 않는 경우 SQL Server에 연결한 후 사용 하도록 설정 하려면 "사용" 단추를 클릭 수 있습니다.

![포털 사용 확장](media/portal-enable-scale-out.PNG) 
## <a name="view-scale-out-master-status"></a>스케일 아웃 마스터 상태 보기
스케일 아웃 마스터의 상태에 표시 되는 **대시보드** 페이지.

![포털의 대시보드](media/portal-dashboard.PNG)
## <a name="view-scale-out-worker-status"></a>스케일 아웃 작업자 상태 보기
스케일 아웃 작업자의 상태에 표시 되는 **작업자 관리자** 페이지. 개별 상태를 보려면 각 작업자를 클릭할 수 있습니다.

![작업자 관리자 포털](media/portal-worker-manager.PNG)

## <a name="add-scale-out-worker"></a>작업자 확장 추가
스케일 아웃 작업자를 추가 하려면 스케일 아웃 작업자 목록 맨 아래에 "+" 단추를 클릭 합니다. 

추가 하 고 "유효성 검사"를 클릭 하려는 아웃 작업자 눈금의 컴퓨터 이름을 입력 하십시오. 스케일 아웃 관리자 스케일 아웃 마스터 및 스케일 아웃 작업자의 컴퓨터에 있는 인증서 저장소에 현재 사용자가 액세스 하는 경우 확인 됩니다.

![작업자 연결](media/connect-worker.PNG)

유효성 검사에 통과 하는 경우 스케일 아웃 관리자는 작업자 프로그램 구성 파일을 읽고 작업자의 인증서 지문을 가져오려면 하려고 합니다. 자세한 내용은 참조 [스케일 아웃 작업자](integration-services-ssis-scale-out-worker.md)합니다. 작업자 구성 파일을 읽을 수 없는 경우에 작업자 인증서를 제공 하기 위한 대체 두 가지가 있습니다. 

작업자 인증서의 지문을 직접 입력 하거나 수 있습니다. 

![작업자 인증서 1](media/portal-cert1.PNG)

또는 인증서 파일을 제공 합니다. 

![작업자 인증서 2](media/portal-cert2.PNG)

모든 정보를 수집한 후 스케일 아웃 관리자는 작업을 수행할 수를 제공 합니다. 인증서 설치, 구성 파일 업데이트를 작업자 및 서비스를 다시 시작 작업자 Tyically를 포함합니다. 

![포털 1 확인 추가](media/portal-add-confirm1.PNG)

작업자 인증서를 액세스할 수 없는 경우에 직접 수동으로 업데이트 하 고 worker 서비스를 다시 시작 해야 합니다.

![포털 2 확인 추가](media/portal-add-confirm2.PNG)

확인 확인란을 클릭 하 고 스케일 아웃 작업자를 추가 하기 시작 합니다.

## <a name="delete-scale-out-worker"></a>작업자 확장 삭제
스케일 아웃 작업자를 삭제 하려면 스케일 아웃 작업자를 선택 하 고 클릭는 "-" 단추는 스케일 아웃 작업자 목록의 맨 아래에 있습니다.


## <a name="enabledisable-scale-out"></a>스케일 아웃 사용/사용 안 함
를 사용 하거나 작업자 스케일 아웃을 사용 하지 않도록 설정 하려면 스케일 아웃 작업자를 선택 하 고 "를 사용 하도록 설정 하는 작업자" 또는 "작업자 사용 안 함" 단추를 클릭 합니다. 작업자 상태에 스케일 아웃 관리자 작업자 오프 라인 상태인 경우 그에 따라 변경 됩니다.

## <a name="edit-scale-out-worker-description"></a>스케일 아웃 작업자 설명 편집
스케일 아웃 작업자에 대 한 설명의 편집 하려면 스케일 아웃 작업자를 선택 하 고 "Edit" 단추를 클릭 합니다. 편집을 완료 한 후 "저장" 단추를 클릭 합니다.

![작업자 저장 포털](media/portal-save-worker.PNG)


