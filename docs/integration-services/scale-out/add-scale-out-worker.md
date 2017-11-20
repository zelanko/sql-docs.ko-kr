---
title: "SSIS 확장 작업자 관리자의 확장 된 추가 | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b769236330941a107865a0b133961bce5bf6b85b
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="add-a-scale-out-worker-with-scale-out-manager"></a>관리자에 확장 된 작업자 확장 추가

크게 integration Services 스케일 아웃 관리자를 사용 하 여 복잡성을 기존 범위 확장 환경에 스케일 아웃 작업자를 추가할 필요가 없습니다. 

아래 단계 사용 하면 스케일 아웃 토폴로지에 스케일 아웃 작업자를 추가할 수 있습니다.

## <a name="1-install-scale-out-worker"></a>1. 작업자 확장 설치
SQL Server 설치 마법사에서 Integration Services 및 스케일 아웃 작업자에서 선택 된 **기능 선택** 페이지. 
![기능 선택 작업자](media/feature-select-worker.PNG)

에 **Integration Services 스케일 아웃 구성-작업자 노드** 페이지에서 클릭 "다음" 여기에 구성 하지 않고 사용 하 **스케일 아웃 관리자** 설치 후 구성을 수행 해야 합니다.

설치 마법사를 완료 합니다.

## <a name="2-open-firewall-on-scale-out-master-computer"></a>2. 스케일 아웃 마스터 컴퓨터에서 방화벽을 열으십시오
스케일 아웃 마스터 설치 (기본적으로 8391)와 포트의 SQL Server (기본적으로: 1433)를 하는 동안 지정 된 포트 열기 스케일 아웃 마스터 컴퓨터에서 Windows 방화벽을 사용 합니다.

## <a name="3-add-scale-out-worker-with-scale-out-manager"></a>3. 작업자 관리자의 확장 된 확장 추가
관리자 권한으로 SQL Server Management Studio를 실행 하 고 스케일 아웃 마스터의 SQL Server 인스턴스에 연결 합니다.

마우스 오른쪽 단추로 클릭 **SSISDB** 고 개체 탐색기에서 **스케일 아웃 관리...** . 

![확장 관리](media/manage-scale-out.PNG)

에 꺼낸를 **스케일 아웃 관리자**로 전환 **작업자 관리자**합니다. 클릭 하 고 "+" 단추 작업자 연결 대화 상자에는 지침을 따릅니다. 자세한 내용은 참조 [스케일 아웃 관리자](integration-services-ssis-scale-out-manager.md)합니다.

