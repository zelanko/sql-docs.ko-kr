---
title: SCOM 관리 팩 설치
description: SQL Server PDW System Center Operations Manager (SCOM) 관리 팩을 다운로드 하 여 설치 하려면 다음 단계를 따르세요. 관리 팩은 SCOM의 SQL Server PDW를 모니터링 하는 데 필요 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: c4cdbd3a640e49bc9a43e30d4bf98cff7bf71194
ms.sourcegitcommit: 67befbf7435f256e766bbce6c1de57799e1db9ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/24/2020
ms.locfileid: "92523828"
---
# <a name="install-sql-server-operations-manager-scom-management-packs-for-analytics-platform-system"></a>분석 플랫폼 시스템용 SCOM (SQL Server Operations Manager) 관리 팩 설치
SQL Server PDW System Center Operations Manager (SCOM) 관리 팩을 다운로드 하 여 설치 하려면 다음 단계를 따르세요. 관리 팩은 SCOM의 SQL Server PDW를 모니터링 하는 데 필요 합니다.  
  
## <a name="before-you-begin"></a><a name="BeforeBegin"></a>시작하기 전 주의 사항  
**전제 조건**  
  
System Center Operations Manager를 설치 하 고 실행 해야 합니다. SQL Server PDW 2012에 System Center Operations Manager 2007 R2, System Center Operations Manager 2012 또는 System Center Operations Manager 2012 Service Pack 1이 필요 합니다.  
  
## <a name="step-1-download-the-management-packs"></a><a name="Step1"></a>1 단계: 관리 팩 다운로드  
APS PDW 워크 로드의 경우 [Microsoft Analytics Platform System 용 System Center 관리 팩](https://go.microsoft.com/fwlink/?LinkId=396857)을 다운로드 합니다.  
  
어플라이언스 관리의 경우 [SQL Server 어플라이언스 기본 관리 팩](/previous-versions/system-center/packs/gg602398(v=technet.10))을 다운로드 합니다.  
  
APS가 없는 이전 버전의 PDW의 경우[Microsoft SQL Server 2012 병렬 데이터 웨어하우스 어플라이언스 용 System Center 모니터링 팩](./download-and-apply-microsoft-updates.md?view=aps-pdw-2016-au7)을 다운로드 합니다.  
  
<!-- MISSING LINKS - For the HDInsight workload, download the [System Center Management Pack for HDInsight](https://go.microsoft.com/fwlink/?LinkId=390208).  -->
  
## <a name="step-2-install-the-management-packs"></a><a name="Step2"></a>2 단계: 관리 팩 설치  
  
### <a name="install-the-sql-server-appliance-base-management-pack"></a>SQL Server 어플라이언스 기본 관리 팩을 설치 합니다.  
  
1.  설치를 실행 하려면 다운로드 한 SQL Server 어플라이언스 기본 관리 팩을 두 번 클릭 합니다.  
  
2.  사용권 계약에 동의 하 고 **다음**을 클릭 합니다.  
  
    ![사용권 계약에 동의 합니다.](./media/install-the-scom-management-packs/SCOM_licnse_agrmt.png "SCOM_licnse_agrmt")  
  
3.  사용자 고유의 설치 폴더를 선택 하거나 기본 관리 팩 설치 폴더를 사용 합니다.  
  
    ![설치 폴더 선택](./media/install-the-scom-management-packs/SCOM_licnse_agrmt2.png "SCOM_licnse_agrmt2")  
  
4.  **Install**을 클릭합니다.  
  
    ![설치 옵션의 설치 확인 단계에서 빨간색 원으로 원으로 설정 된 SQL Server 어플라이언스 기본 모니터링 MP 설치 마법사의 스크린샷](./media/install-the-scom-management-packs/SCOM_licnse_agrmt3.png "SCOM_licnse_agrmt3")  
  
5.  **닫기**를 클릭합니다.  
  
    ![닫기 클릭](./media/install-the-scom-management-packs/SCOM_licnse_agrmt4.png "SCOM_licnse_agrmt4")  
  
### <a name="install-the-monitoring-pack-for-sql-server-pdw-appliance"></a>SQL Server PDW 어플라이언스 용 모니터링 팩 설치  
  
1.  설치를 실행 하려면 다운로드 한 SQL Server PDW 어플라이언스 관리 팩을 두 번 클릭 합니다.  
  
2.  사용권 계약에 동의 하 고 **다음**을 클릭 합니다.  
  
    ![사용권 계약에 동의](./media/install-the-scom-management-packs/SCOM_licnse_agmtB.png "SCOM_licnse_agmtB")  
  
3.  압축을 푼 파일을 저장할 디렉터리를 선택 합니다. 기본적으로 기본 관리 팩 설치 폴더가 표시 됩니다. 기본값을 선택 하거나 설치 폴더를 선택 합니다.  
  
    ![설치 폴더 선택](./media/install-the-scom-management-packs/SCOM_licnse_agmtB1.png "SCOM_licnse_agmtB1")  
  
4.  **Install**을 클릭합니다.  
  
    ![설치 옵션의 설치 확인 단계에서 빨간색 원으로 원으로 설정 된 설치 관리자 마법사의 스크린샷](./media/install-the-scom-management-packs/SCOM_licnse_agmtB2.png "SCOM_licnse_agmtB2")  
  
5.  **닫기**를 클릭합니다.  
  
    ![설치 완료](./media/install-the-scom-management-packs/SCOM_licnse_agmtB3.png "SCOM_licnse_agmtB3")  
  
## <a name="next-step"></a>다음 단계  
관리 팩을 설치 했으므로 다음 단계를 계속 진행 합니다. [PDW 용 SCOM 관리 팩 가져오기 &#40;분석 플랫폼 시스템&#41;](import-the-scom-management-pack-for-pdw.md)합니다.  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->