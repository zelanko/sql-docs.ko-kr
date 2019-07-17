---
title: Reporting Services-보고서 기록에 스냅숏 추가 | Microsoft Docs
ms.prod: reporting-services
ms.technology: reporting-services
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 06/26/2019
ms.openlocfilehash: e7244e66ec8f6aabd7684bbcd5c22e8d2604d1cb
ms.sourcegitcommit: c0e48b643385ce19c65ca6e348ce83b2d22b6514
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67492840"
---
# <a name="add-a-snapshot-to-report-history"></a>보고서 기록에 스냅샷 추가

보고서 기록은 시간에 따라 만든 보고서 스냅샷의 모음입니다. 보고서 스냅샷은 레이아웃 정보 및 특정 시점에 검색된 쿼리 결과가 들어 있는 보고서입니다. 보고서를 선택할 때 최신 쿼리 결과를 얻을 수 있는 요청 시 실행 보고서와 달리 보고서 스냅샷은 예약된 시간에 처리되고 보고서 서버에 저장됩니다. 표시할 보고서 스냅샷을 선택하면 보고서 서버가 보고서 서버 데이터베이스에서 저장된 보고서를 검색하고 스냅샷이 만들어진 시점에 따른 보고서의 현재 데이터 및 레이아웃을 표시합니다.  
  
보고서 스냅샷은 특정 렌더링 형식으로 저장되지 않으며 사용자나 애플리케이션이 보고서 스냅샷을 요청할 때만 HTML과 같은 최종 보기 형식으로 렌더링됩니다. 지연된 렌더링은 스냅샷을 이동 가능하게 만듭니다. 요청 디바이스나 웹 브라우저에 적합한 형식으로 보고서를 렌더링할 수 있습니다.  
  
## <a name="to-manually-add-snapshots-to-report-history"></a>보고서 기록에 스냅샷을 수동으로 추가하려면
  
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

1. 보고서 관리자에서 **내용** 페이지로 이동하고 기록을 보려는 항목을 마우스로 가리킨 다음 드롭다운 화살표를 클릭합니다.
  
2. 드롭다운 메뉴에서 **보고서 기록 보기**를 클릭합니다.  
  
3. **새 스냅숏**을 클릭합니다. **실행 날짜** 열에 새 스냅숏이 생성됩니다.  
    > [!NOTE]
    > 관리자가 보고서 기록 스냅숏을 만드는 사용 하려면 구성 해야 합니다 **수동으로 기록 허용**합니다. 자세한 내용은 [보고서 기록 제한&#40;보고서 관리자&#41;](../reports/limit-report-history-report-manager.md)를 클릭합니다.

4. **적용**을 클릭합니다.
  
## <a name="to-automatically-add-all-snapshots-to-report-history"></a>보고서 기록에 모든 스냅샷을 자동으로 추가하려면  
  
1. 보고서 실행 스냅샷으로 실행하도록 구성된 보고서의 경우 스냅샷이 새로 고쳐질 때마다 보고서 기록에 스냅샷 복사본을 저장하도록 추가 속성을 설정할 수 있습니다.  
  
2. 보고서 관리자에서 **내용** 페이지로 이동하고 기록을 보려는 항목을 마우스로 가리킨 다음 드롭다운 화살표를 클릭합니다.  
  
3. 드롭다운 메뉴에서 **관리**를 클릭합니다.  
  
4. **스냅숏 옵션**을 클릭합니다.  
  
5. **모든 보고서 실행 스냅숏을 기록에 저장**확인란을 선택합니다.  
  
6. **적용**을 클릭합니다.  
  
## <a name="to-automatically-add-snapshots-to-report-history-based-on-a-schedule"></a>일정에 따라 보고서 기록에 스냅샷을 자동으로 추가하려면  
  
1. 보고서 관리자에서 **내용** 페이지로 이동하고 기록을 보려는 항목을 마우스로 가리킨 다음 드롭다운 화살표를 클릭합니다.  
  
2. 드롭다운 메뉴에서 **관리**를 클릭합니다.  
  
3. **스냅숏 옵션**을 클릭합니다.  
  
4. **다음 일정을 사용하여 스냅숏을 보고서 기록에 추가**확인란을 선택합니다. 다음 중 하나를 수행합니다.  
  
    - **보고서별 일정**을 선택합니다. 일정 정보를 채우고 일정의 시작일과 종료일을 선택한 후 **확인**을 클릭합니다.  

    - **공유 일정**을 선택합니다. 목록에서 원하는 일정을 선택합니다.  

5. **적용**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:

- [보고서에 실행 속성 구성&#40;보고서 관리자&#41;](../../reporting-services/reports/configure-execution-properties-for-a-report-report-manager.md)
- [보고서 기록 제한&#40;보고서 관리자&#41;](../../reporting-services/reports/limit-report-history-report-manager.md)
- [일정](../../reporting-services/subscriptions/schedules.md)   
- [보고서 관리자&#40;SSRS 기본 모드&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

## <a name="to-manually-add-snapshots-to-report-history"></a>보고서 기록에 스냅샷을 수동으로 추가하려면
  
1. 웹 포털에서의 기록을 보려면 마우스 오른쪽 단추로 클릭 하려는 항목으로 이동 합니다.  
  
2. 드롭다운 메뉴에서 **관리**를 선택합니다.  
  
3. 선택 된 **기록 스냅숏** 탭 합니다.  
  
4. 에 **기록 스냅숏** 페이지에서 선택 합니다 **새 기록 스냅숏**. 새 스냅숏이 생성 되 고 현재 날짜 및 시간을 사용 하 여 아래에 표시 합니다 **Created** 열입니다.  
  
    > [!NOTE]
    > 관리자가 보고서 기록 스냅숏을 만드는 사용 하려면 구성 해야 합니다 **수동으로 기록 허용**합니다. 자세한 내용은 [보고서 기록 제한 (웹 포털)](../../reporting-services/reports/limit-report-history-report-manager.md)합니다.

## <a name="to-add-snapshots-via-a-schedule-to-report-history"></a>일정을 통해 스냅숏을 보고서 기록에 추가 하려면

1. 웹 포털에서의 기록을 보려면 마우스 오른쪽 단추로 클릭 하려는 항목으로 이동 합니다.  
  
2. 드롭다운 메뉴에서 **관리**를 선택합니다.  
  
3. 선택 된 **기록 스냅숏** 탭 합니다.  
  
4. 에 **기록 스냅숏** 페이지에서 선택 합니다 **일정 및 설정** 단추.  
  
5. 에 **일정** 섹션, 하나 이상의 선택한 아직 선택 하지 않은 경우 아래 옵션 중 하나 또는 모두를 선택 합니다.
    - **일정에 따라 기록 스냅숏 만들기**합니다.  
    - **사람들이 스냅숏을 수동으로 만들 수 있도록**입니다.  
  
6. 에 **고급** 섹션에서 **모든 기록 스냅숏을 보존**합니다.  
  
7. 필요에 따라 확인란을 선택 **보고서 기록에 캐시 스냅숏도 저장**합니다.  
  
8.  **적용**을 선택하여 설정을 저장합니다.  

    > [!NOTE]  
    > 관리자가 보고서 기록 스냅숏을 만드는 사용 하려면 구성 해야 합니다 **수동으로 기록 허용**합니다. 자세한 내용은 [보고서 기록 제한 (웹 포털)](../../reporting-services/reports/limit-report-history-report-manager.md)합니다.

9.  **적용**을 클릭합니다.

## <a name="to-automatically-add-all-snapshots-to-report-history"></a>보고서 기록에 모든 스냅샷을 자동으로 추가하려면  
  
1. 보고서 실행 스냅샷으로 실행하도록 구성된 보고서의 경우 스냅샷이 새로 고쳐질 때마다 보고서 기록에 스냅샷 복사본을 저장하도록 추가 속성을 설정할 수 있습니다.  
  
2. 웹 포털에서의 기록을 보려면 마우스 오른쪽 단추로 클릭 하려는 항목으로 이동 합니다.  
  
3. 드롭다운 메뉴에서 **관리**를 선택합니다.  
  
4. 선택 된 **기록 스냅숏** 탭 합니다.  
  
5. 에 **기록 스냅숏** 페이지에서 선택 합니다 **일정 및 설정** 단추.  
  
6. 에 **일정** 섹션, 하나 이상의 선택한 아직 선택 하지 않은 경우 아래 옵션 중 하나 또는 모두를 선택 합니다.
    - **일정에 따라 기록 스냅숏 만들기**합니다.  
    - **사람들이 스냅숏을 수동으로 만들 수 있도록**입니다.  
  
7. 에 **고급** 섹션에서 **모든 기록 스냅숏을 보존**합니다.  
  
8. 필요에 따라 확인란을 선택 **보고서 기록에 캐시 스냅숏도 저장**합니다.  
  
9. **적용**을 선택하여 설정을 저장합니다.  
  
## <a name="to-automatically-add-snapshots-to-report-history-based-on-a-schedule"></a>일정에 따라 보고서 기록에 스냅샷을 자동으로 추가하려면  
  
1. 웹 포털에서의 기록을 보려면 마우스 오른쪽 단추로 클릭 하려는 항목으로 이동 합니다.  
  
2. 드롭다운 메뉴에서 **관리**를 선택합니다.  
  
3. 선택 된 **기록 스냅숏** 탭 합니다.  
  
4. 에 **기록 스냅숏** 페이지에서 선택 합니다 **일정 및 설정** 단추.  
  
5. **다음 일정을 사용하여 스냅숏을 보고서 기록에 추가**확인란을 선택합니다. 다음 중 하나를 수행합니다.  
  
    - **보고서별 일정**을 선택합니다. 일정 정보를 채우고 일정의 시작일과 종료일을 선택한 후 **확인**을 클릭합니다.  

    - **공유 일정**을 선택합니다. 목록에서 원하는 일정을 선택합니다.  

5. **적용**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:

- [보고서 실행 속성 구성(웹 포털)](../../reporting-services/reports/configure-execution-properties-for-a-report-report-manager.md)
- [보고서 기록을 (웹 포털) 제한](../../reporting-services/reports/limit-report-history-report-manager.md)
- [일정](../../reporting-services/subscriptions/schedules.md)   
- [웹 포털 &#40;SSRS 기본 모드&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)

::: moniker-end