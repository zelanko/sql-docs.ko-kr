---
title: SCOM 관리 팩 인 Analytics Platform System 설치 | Microsoft Docs
description: 다운로드 하 여 SQL Server PDW 용 System Center Operations Manager (SCOM) 관리 팩을 설치 하려면 다음이 단계를 따릅니다. 관리 팩은 SQL Server PDW SCOM에서 모니터링 해야 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f0acfa636a3432dcffb18cfec57ee7625c1eb01b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63215576"
---
# <a name="install-sql-server-operations-manager-scom-management-packs-for-analytics-platform-system"></a>Analytics Platform System에 대 한 SQL Server Operations Manager (SCOM) 관리 팩을 설치 합니다.
다운로드 하 여 SQL Server PDW 용 System Center Operations Manager (SCOM) 관리 팩을 설치 하려면 다음이 단계를 따릅니다. 관리 팩은 SQL Server PDW SCOM에서 모니터링 해야 합니다.  
  
## <a name="BeforeBegin"></a>시작하기 전 주의 사항  
**필수 구성 요소**  
  
System Center Operations Manager는 설치 하 고 실행 해야 합니다. SQL Server PDW 2012 System Center Operations Manager 2007 R2, System Center Operations Manager 2012 또는 System Center Operations Manager 2012 서비스 팩 1에 필요합니다.  
  
## <a name="Step1"></a>1 단계: 관리 팩 다운로드  
AP PDW 워크 로드의 경우 다운로드 합니다 [Microsoft Analytics Platform System에 대 한 System Center 관리 팩](https://go.microsoft.com/fwlink/?LinkId=396857)합니다.  
  
어플라이언스 관리에 대 한 다운로드 합니다 [SQL Server 어플라이언스 기본 관리 팩](https://www.microsoft.com/download/details.aspx?displaylang=en&id=11436)합니다.  
  
AP 없이 PDW의 이전 버전을 다운로드 합니다[Microsoft SQL Server 2012 병렬 데이터 웨어하우스 어플라이언스 용 System Center 모니터링 팩](https://go.microsoft.com/fwlink/p/?LinkId=282661)합니다.  
  
<!-- MISSING LINKS - For the HDInsight workload, download the [System Center Management Pack for HDInsight](https://go.microsoft.com/fwlink/?LinkId=390208).  -->
  
## <a name="Step2"></a>2 단계: 관리 팩 설치  
  
### <a name="install-the-sql-server-appliance-base-management-pack"></a>SQL Server 어플라이언스의 기본 관리 팩 설치  
  
1.  설치를 실행 하려면 다운로드 한 SQL Server 어플라이언스 기본 관리 팩을 두 번 클릭 합니다.  
  
2.  사용권 계약에 동의 하 고 클릭 **다음**합니다.  
  
    ![사용권 계약에 동의](./media/install-the-scom-management-packs/SCOM_licnse_agrmt.png "SCOM_licnse_agrmt")  
  
3.  사용자 고유의 설치 폴더를 선택 하거나 기본 관리 팩 설치 폴더를 사용 합니다.  
  
    ![설치 폴더 선택](./media/install-the-scom-management-packs/SCOM_licnse_agrmt2.png "SCOM_licnse_agrmt2")  
  
4.  **설치**를 클릭합니다.  
  
    ![설치 확인](./media/install-the-scom-management-packs/SCOM_licnse_agrmt3.png "SCOM_licnse_agrmt3")  
  
5.  **닫기**를 클릭합니다.  
  
    ![닫기를 클릭](./media/install-the-scom-management-packs/SCOM_licnse_agrmt4.png "SCOM_licnse_agrmt4")  
  
### <a name="install-the-monitoring-pack-for-sql-server-pdw-appliance"></a>SQL Server PDW 어플라이언스에 용 모니터링 팩 설치  
  
1.  설치를 실행 하려면 다운로드 한 SQL Server PDW 어플라이언스 관리 팩을 두 번 클릭 합니다.  
  
2.  사용권 계약에 동의 하 고 클릭 **다음**합니다.  
  
    ![사용권 계약에 동의](./media/install-the-scom-management-packs/SCOM_licnse_agmtB.png "SCOM_licnse_agmtB")  
  
3.  압축 푼된 파일을 포함 하는 디렉터리를 선택 합니다. 기본 관리 팩 설치 폴더는 기본적으로 표시 됩니다. 기본 또는 사용자 고유의 설치 폴더를 선택 합니다.  
  
    ![설치 폴더 선택](./media/install-the-scom-management-packs/SCOM_licnse_agmtB1.png "SCOM_licnse_agmtB1")  
  
4.  **설치**를 클릭합니다.  
  
    ![설치 확인](./media/install-the-scom-management-packs/SCOM_licnse_agmtB2.png "SCOM_licnse_agmtB2")  
  
5.  **닫기**를 클릭합니다.  
  
    ![설치 완료](./media/install-the-scom-management-packs/SCOM_licnse_agmtB3.png "SCOM_licnse_agmtB3")  
  
## <a name="next-step"></a>다음 단계  
관리 팩을 설치 했으므로 다음 단계를 계속 합니다. [PDW 용 SCOM 관리 팩 가져오기 &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md)합니다.  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
