---
title: "단일 컴퓨터에서 SSIS 눈금 시작 | Microsoft Docs"
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
ms.openlocfilehash: 7175c63be4c0e15e50f2020f75d283ac0e3dfdbf
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="get-started-with-integration-services-ssis-scale-out-on-a-single-computer"></a>시작 눈금 Integration Services (SSIS)는 단일 컴퓨터에서 아웃
이 섹션에서는 기본 설정으로는 1-(1-box) 환경에서 Integration Services 스케일 아웃를 설정의 안내를 제공 합니다.

## <a name="1-install-sql-server-features"></a>1. SQL Server 기능 설치
SQL Server 설치 마법사에서 데이터베이스 엔진 서비스, Integration Services, 스케일 아웃 마스터 및 스케일 아웃 작업자에서 선택 된 **기능 선택** 페이지.

![기능 선택 Onebox 1](media/feature-select-onebox1.PNG)

![기능 선택 Onebox 2](media/feature-select-onebox2.PNG)

에 **서버 구성** 페이지, "다음" 시작 유형 및 기본 서비스 계정을 사용 하 여 클릭 합니다.

에 **데이터베이스 엔진 구성** 페이지에서 "**혼합 모드**"및 클릭"**현재 사용자 추가**" 단추입니다. 

![엔진 구성](media/engine-config.PNG)

하나는 **Integration Services 스케일 아웃 구성-마스터 노드** 및 **Integration Services 스케일 아웃 구성-작업자 노드** 페이지, 포트 및 인증서의 기본 설정을 적용 하려면 "다음"를 클릭 하기만 하면 됩니다.

SQL Server 설치 마법사를 완료 합니다.

## <a name="2-install-sql-server-management-studio"></a>2. SQL Server Management Studio를 설치 합니다.

[다운로드](../../ssms/download-sql-server-management-studio-ssms.md) SQL Server Management Studio 하 고 설치 합니다.

## <a name="3-enable-scale-out"></a>3. 확장을 사용 하도록 설정
SSMS를 열고 로컬 Sql Server 인스턴스에 연결 합니다.
마우스 오른쪽 단추로 클릭 **Integration Services 카탈로그** 고 개체 탐색기에서 **카탈로그 만들기**합니다.

에 **카탈로그 만들기** 대화 상자에서 **마스터 SSIS 수평적으로이 서버를 사용 하도록 설정** 기본적으로 선택 됩니다. 카탈로그를 일반적인 방식으로 만듭니다. 

## <a name="4-enable-scale-out-worker"></a>4. 작업자 확장을 사용 하도록 설정
SSMS에서 **SSISDB** 선택 **스케일 아웃 관리...** . 
![확장 관리](media/manage-scale-out.PNG)

에서는 Integration Services 스케일 아웃 관리자 팝업 됩니다. 범위 확장 함께 관리할 수 있습니다. 자세한 내용은 참조 [Integration Services 스케일 아웃 관리자](integration-services-ssis-scale-out-manager.md)합니다.

스케일 아웃 작업자를 사용 하도록 설정 하려면 전환 **작업자 관리자** 하 고 사용 하도록 설정 하려는 작업자를 선택 합니다. 작업자는 원래 사용할 수 없습니다. 클릭 **사용 작업자** 사용 하도록 설정 합니다.

## <a name="5-run-packages-in-scale-out"></a>5. 규모 확장에서 패키지 실행
이제 범위 확장에서 SSIS 패키지를 실행할 준비가 되었습니다. 참조 [Integration services (SSIS) 패키지를 실행할된 확장할](run-packages-in-integration-services-ssis-scale-out.md)합니다.


더 많은 범위 확장 작업자를 추가 하려면 참조 [스케일 아웃 관리자와 스케일 아웃 자가 추가](add-scale-out-worker.md)합니다.
