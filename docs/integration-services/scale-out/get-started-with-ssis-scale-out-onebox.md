---
title: "단일 컴퓨터에서 SSIS Scale Out 시작| Microsoft Docs"
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
ms.openlocfilehash: 8514cd548b003a39bf198b83b6b80d775a55384b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="get-started-with-integration-services-ssis-scale-out-on-a-single-computer"></a>단일 컴퓨터에서 Integration Services(SSIS) Scale Out 시작
이 섹션에서는 단일 상자 환경에서 기본 설정을 사용하여 Integration Services Scale Out을 설정하는 방법을 안내합니다.

## <a name="1-install-sql-server-features"></a>1. SQL Server 기능 설치
SQL Server 설치 마법사의 **기능 선택** 페이지에서 데이터베이스 엔진 서비스, Integration Services, Scale Out 마스터 및 Scale Out 작업자를 선택합니다.

![기능 선택 Onebox 1](media/feature-select-onebox1.PNG)

![기능 선택 Onebox 2](media/feature-select-onebox2.PNG)

**서버 구성** 페이지에서 "다음"을 클릭하여 기본 서비스 계정 및 시작 유형을 사용합니다.

**데이터베이스 엔진 구성** 페이지에서 "**혼합 모드**"를 클릭하고 "**현재 사용자 추가**" 단추를 클릭합니다. 

![엔진 구성](media/engine-config.PNG)

**Integration Services Scale Out 구성 - 마스터 노드** 및 **Integration Services Scale Out 구성 - 작업자 노드** 페이지에서 "다음"을 클릭하여 포트 및 인증서의 기본 설정을 적용합니다.

SQL Server 설치 마법사를 완료합니다.

## <a name="2-install-sql-server-management-studio"></a>2. SQL Server Management Studio 설치

SQL Server Management Studio를 [다운로드](../../ssms/download-sql-server-management-studio-ssms.md)하여 설치합니다.

## <a name="3-enable-scale-out"></a>3. Scale Out을 사용하도록 설정
SSMS를 열고 로컬 Sql Server 인스턴스에 연결합니다.
개체 탐색기에서 **Integration Services 카탈로그**를 마우스 오른쪽 단추로 클릭하고 **카탈로그 만들기**를 선택합니다.

**카탈로그 만들기** 대화 상자에서 **이 서버를 SSIS Scale Out 마스터로 사용**이 기본적으로 선택됩니다. 평소와 같이 카탈로그를 만듭니다. 

## <a name="4-enable-scale-out-worker"></a>4. Scale Out 작업자를 사용하도록 설정
SSMS에서 **SSISDB**를 마우스 오른쪽 단추로 클릭하고 **Scale Out 관리...**를 선택합니다. ![Scale Out 관리](media/manage-scale-out.PNG)

Integration Services Scale Out 관리자가 나타납니다. 여기서 Scale Out을 관리할 수 있습니다. 자세한 내용은 [Integration Services Scale Out 관리자](integration-services-ssis-scale-out-manager.md)를 참조하세요.

Scale Out 작업자를 사용하도록 설정하려면 **작업자 관리자**로 전환하고 사용하도록 설정할 작업자를 선택합니다. 작업자는 기본적으로 사용되지 않습니다. **작업자 사용**을 클릭하여 사용하도록 설정합니다.

## <a name="5-run-packages-in-scale-out"></a>5. 규모 확장에서 패키지 실행
이제 Scale Out에서 SSIS 패키지를 실행할 준비가 완료되었습니다. [Integration Services(SSIS) Scale Out에서 패키지 실행](run-packages-in-integration-services-ssis-scale-out.md)을 참조하세요.


더 많은 Scale Out 작업자를 추가하려면 [Scale Out 관리자를 사용하여 Scale Out 작업자 추가](add-scale-out-worker.md)를 참조하세요.
