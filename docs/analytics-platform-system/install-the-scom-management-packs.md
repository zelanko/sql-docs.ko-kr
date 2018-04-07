---
title: SCOM 관리 팩 (분석 플랫폼 시스템)를 설치 합니다.
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab3985d8-0a71-4b28-9d28-9886ae2a110f
caps.latest.revision: 16
ms.openlocfilehash: 2f05a947f09940fc1dd676ec6ca316863f567a7f
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="install-the-scom-management-packs"></a>SCOM 관리 팩을 설치
다음 단계를 다운로드 하 여 SQL Server PDW에 대 한 System Center Operations Manager (SCOM) 관리 팩을 설치 합니다. 관리 팩은 SCOM에서 SQL Server PDW 모니터링 해야 합니다.  
  
## <a name="BeforeBegin"></a>시작하기 전 주의 사항  
**필수 구성 요소**  
  
System Center Operations Manager 설치 및 실행 되어야 합니다. SQL Server PDW 2012 System Center Operations Manager 2007 R2, System Center Operations Manager 2012 또는 System Center Operations Manager 2012 서비스 팩 1에 필요합니다.  
  
## <a name="Step1"></a>1 단계: 관리 팩을 다운로드  
APS PDW 작업에 대 한 다운로드는 [Microsoft 분석 플랫폼 시스템에 대 한 System Center 관리 팩](http://go.microsoft.com/fwlink/?LinkId=396857)합니다.  
  
어플라이언스 관리에 대 한 다운로드는 [SQL Server 어플라이언스의 기본 관리 팩](http://www.microsoft.com/en-us/download/details.aspx?displaylang=en&id=11436)합니다.  
  
PDW 없이 APS의 이전 버전에 대 한 다운로드는[Microsoft SQL Server 2012 병렬 데이터 웨어하우스 어플라이언스 용 System Center 모니터링 팩](http://go.microsoft.com/fwlink/p/?LinkId=282661)합니다.  
  
HDInsight 작업에 대 한 다운로드는 [HDInsight에 대 한 System Center 관리 팩](http://go.microsoft.com/fwlink/?LinkId=390208)합니다.  
  
## <a name="Step2"></a>관리 팩을 설치 하는 2 단계:  
  
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
  
### <a name="install-the-monitoring-pack-for-sql-server-pdw-appliance"></a>SQL Server PDW 어플라이언스 용 모니터링 팩을 설치 합니다.  
  
1.  설치를 실행 하려면 다운로드 한 SQL Server PDW 어플라이언스에 관리 팩을 두 번 클릭 합니다.  
  
2.  사용권 계약에 동의 하 고 클릭 **다음**합니다.  
  
    ![라이선스 함 수락](./media/install-the-scom-management-packs/SCOM_licnse_agmtB.png "SCOM_licnse_agmtB")  
  
3.  압축 푼된 파일을 저장할 디렉터리를 선택 합니다. 기본 관리 팩 설치 폴더는 기본적으로 표시 됩니다. 기본적으로 또는 사용자 고유의 설치 폴더를 선택 합니다.  
  
    ![설치 폴더 선택](./media/install-the-scom-management-packs/SCOM_licnse_agmtB1.png "SCOM_licnse_agmtB1")  
  
4.  **설치**를 클릭합니다.  
  
    ![설치 확인](./media/install-the-scom-management-packs/SCOM_licnse_agmtB2.png "SCOM_licnse_agmtB2")  
  
5.  **닫기**를 클릭합니다.  
  
    ![설치 완료](./media/install-the-scom-management-packs/SCOM_licnse_agmtB3.png "SCOM_licnse_agmtB3")  
  
## <a name="next-step"></a>다음 단계  
설치 된 관리 팩 설정 했으므로 다음 단계를 계속: [PDW에 대 한 SCOM 관리 팩을 가져올 &#40;분석 플랫폼 시스템&#41;](import-the-scom-management-pack-for-pdw.md)합니다.  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
