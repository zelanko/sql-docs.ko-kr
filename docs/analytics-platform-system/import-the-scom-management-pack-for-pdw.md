---
title: SCOM 관리 팩 가져오기
description: 다음 단계를 수행 하 여 APS (Analytics Platform System) 용 SCOM (System Center Operations Manager) 관리 팩을 가져옵니다. 관리 팩은 SCOM에서 병렬 데이터 웨어하우스를 모니터링 하는 데 필요 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: bcb0e667424767fd53a5fc7e027e84d512022203
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401080"
---
# <a name="import-the-scom-management-pack---analytics-platform-system"></a>SCOM 관리 팩-분석 플랫폼 시스템 가져오기
다음 단계를 수행 하 여 APS (Analytics Platform System) 용 SCOM (System Center Operations Manager) 관리 팩을 가져옵니다. 관리 팩은 SCOM에서 병렬 데이터 웨어하우스를 모니터링 하는 데 필요 합니다. 
  
## <a name="before-you-begin"></a><a name="BeforeBegin"></a>시작 하기 전에  
**필수 구성 요소**  
  
System Center Operations Manager 2007 r 2를 설치 하 고 실행 해야 합니다.  
  
관리 팩을 설치 해야 합니다. [&#40;분석 플랫폼 시스템&#41;SCOM 관리 팩 설치를 ](install-the-scom-management-packs.md)참조 하세요.  
  
## <a name="step-1-import-the-sql-server-appliance-base-management-pack"></a><a name="Step1"></a>1 단계: SQL Server 어플라이언스 기본 관리 팩 가져오기  
  
1.  Operations Manager 2007 관리 그룹에 대해 Operations Manager 관리자 역할의 구성원 계정으로 컴퓨터에 로그온합니다.  
  
2.  운영 콘솔에서 **관리**를 클릭합니다.  
  
3.  **관리 팩** 노드를 마우스 오른쪽 단추로 클릭한 후 **관리 팩 가져오기**를 클릭합니다.  
  
    ![관리 팩 가져오기 클릭](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP.png "SCOM_IMP")  
  
4.  관리 팩 목록에서 가져올 관리 팩을 선택하고 **선택**, **추가**를 차례로 클릭합니다.  
  
    ![관리 팩 목록](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP2.png "SCOM_IMP2")  
  
5.  **어플라이언스** 를 검색 한 다음 SQL Server 어플라이언스 기반으로 드릴 다운 하 고 두 가지 선택 항목 **추가** 를 클릭 합니다.  
  
    ![SQL Server 어플라이언스 기준](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP3.png "SCOM_IMP3")  
  
6.  두 관리 팩이 선택한 아래쪽 창에 있는 경우 **확인**을 클릭 합니다.  
  
    ![두 관리 팩 모두 선택](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP4.png "SCOM_IMP4")  
  
7.  **Install**을 클릭합니다.  
  
    ![설치 클릭](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP5.png "SCOM_IMP5")  
  
8.  완료 되 면 **닫기**를 클릭 합니다.  
  
    ![완료되면 닫기를 클릭](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP6.png "SCOM_IMP6")  
  
## <a name="import-the-monitoring-pack-for-microsoft-sql-server-2008-r2-parallel-data-warehouse-appliance"></a><a name="Step2"></a>Microsoft SQL Server 2008 R2 병렬 데이터 웨어하우스 어플라이언스 용 모니터링 팩 가져오기  
  
1.  **관리 팩** 노드를 마우스 오른쪽 단추로 클릭한 후 **관리 팩 가져오기**를 클릭합니다.  
  
2.  **디스크에서 추가**...를 선택 합니다.  
  
    ![관리 팩을 마우스 오른쪽 단추로 클릭](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW.png "SCOM_PDW")  
  
3.  SQL Server PDW 관리 팩을 추출한 위치로 이동 하 고 "가져올 관리 팩을 선택 하십시오." 섹션에 있는 세 개의 관리 팩을 선택 합니다. 첫 번째 항목을 선택 하 고 Shift를 클릭 한 다음 마지막 항목을 선택 하 여이 작업을 수행할 수 있습니다. 모두 선택 했으면 **열기**를 클릭 합니다.  
  
    ![관리 팩 선택](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW2.png "SCOM_PDW2")  
  
4.  **Install**을 클릭합니다.  
  
    ![설치 클릭](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW3.png "SCOM_PDW3")  
  
5.  **닫기**를 클릭합니다.  
  
    ![닫기 클릭](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW4.png "SCOM_PDW4")  
  
## <a name="next-step"></a>다음 단계  
관리 팩을 가져온 후에는 다음 단계를 계속 진행 합니다. [분석 플랫폼 시스템 &#40;분석 플랫폼 시스템&#41;을 모니터링 하도록 SCOM을 구성 ](configure-scom-to-monitor-analytics-platform-system.md)합니다.  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
