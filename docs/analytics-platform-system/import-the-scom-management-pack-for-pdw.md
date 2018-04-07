---
title: PDW (분석 플랫폼 시스템)에 대 한 SCOM 관리 팩 가져오기
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
ms.assetid: fa735041-8e58-4886-ae3b-36f3c6298b12
caps.latest.revision: 6
ms.openlocfilehash: d8accd7106cce2274e60793e123779e87b8dfd49
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="import-the-scom-management-pack-for-pdw"></a>PDW에 대 한 SCOM 관리 팩 가져오기
SQL Server PDW에 대 한 System Center Operations Manager (SCOM) 관리 팩을 가져오려면 다음이 단계를 수행 합니다. 관리 팩은 SCOM에서 SQL Server PDW 모니터링 해야 합니다.  
  
## <a name="BeforeBegin"></a>시작하기 전 주의 사항  
**필수 구성 요소**  
  
System Center Operations Manager 2007 r 2는 설치 되어 실행 중 이어야 합니다.  
  
관리 팩이 설치 해야 합니다. 참조 [SCOM 관리 팩을 설치 &#40;분석 플랫폼 시스템&#41;](install-the-scom-management-packs.md)합니다.  
  
## <a name="Step1"></a>1 단계: SQL Server 어플라이언스 기본 관리 팩 가져오기  
  
1.  Operations Manager 2007 관리 그룹에 대 한 Operations Manager 관리자 역할의 구성원 인 계정으로 컴퓨터에 로그온 합니다.  
  
2.  운영 콘솔에서 클릭 **관리**합니다.  
  
3.  마우스 오른쪽 단추로 클릭는 **관리 팩** 노드를 차례로 클릭 한 다음 **관리 팩 가져오기**합니다.  
  
    ![관리 팩 가져오기 클릭](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP.png "SCOM")  
  
4.  관리 팩 목록에서 관리 팩을 가져오려면 클릭 선택 **선택**, 클릭 하 고 **추가**합니다.  
  
    ![관리 팩 목록](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP2.png "SCOM_IMP2")  
  
5.  검색할 **기기** 및 SQL Server 어플라이언스 자료로 드릴 다운 하 여 클릭 **추가** 두 가지 선택 합니다.  
  
    ![SQL Server 어플라이언스 기준](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP3.png "SCOM_IMP3")  
  
6.  선택한 아래쪽 창에 두 개의 관리 팩 인 되 면 클릭 **확인**합니다.  
  
    ![관리 팩 모두 선택](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP4.png "SCOM_IMP4")  
  
7.  **설치**를 클릭합니다.  
  
    ![설치 클릭](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP5.png "SCOM_IMP5")  
  
8.  완료 되 면 클릭 **닫기**합니다.  
  
    ![완료 되 면 닫기를 클릭](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP6.png "SCOM_IMP6")  
  
## <a name="Step2"></a>Microsoft SQL Server 2008 R2 병렬 데이터 웨어하우스 어플라이언스에 대 한 모니터링 팩을 가져오고  
  
1.  마우스 오른쪽 단추로 클릭는 **관리 팩** 노드를 차례로 클릭 한 다음 **관리 팩 가져오기**합니다.  
  
2.  선택 **디스크에서 추가**...  
  
    ![관리 팩을 마우스 오른쪽 단추로 클릭](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW.png "SCOM_PDW")  
  
3.  SQL Server PDW 관리 팩의 압축을 푼 위치로 이동한 다음 "선택한 관리 팩을 가져오는" 섹션에 있는 세 개의 관리 팩을 선택 합니다. 첫 번째 템플릿을 선택, Shift를 클릭 하 고 마지막을 선택 하 여이 수행할 수 있습니다. 모두 선택를 클릭 **열려**합니다.  
  
    ![관리 팩 선택](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW2.png "SCOM_PDW2")  
  
4.  **설치**를 클릭합니다.  
  
    ![설치 클릭](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW3.png "SCOM_PDW3")  
  
5.  **닫기**를 클릭합니다.  
  
    ![닫기를 클릭](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW4.png "SCOM_PDW4")  
  
## <a name="next-step"></a>다음 단계  
관리 팩을 가져온 했으므로 다음 단계를 계속: [모니터 분석 플랫폼 시스템에 구성 SCOM &#40;분석 플랫폼 시스템&#41;](configure-scom-to-monitor-analytics-platform-system.md)합니다.  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
