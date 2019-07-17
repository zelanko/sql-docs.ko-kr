---
title: 데이터 기반 구독 만들기, 수정 및 삭제 | Microsoft Docs
ms.date: 06/12/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- query-based subscriptions [Reporting Services]
- queries [Reporting Services], data-driven subscriptions
- subscriptions [Reporting Services], data-driven
- data-driven subscriptions
ms.assetid: 0ba2093e-9393-4eb6-af06-9da10988cfaf
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b385e04cf2efa103dba4a66d4e794a7984814fb4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "67140265"
---
# <a name="create-modify-and-delete-data-driven-subscriptions"></a>데이터 기반 구독 만들기, 수정 및 삭제
  데이터 기반 구독은 런타임에 구독을 처리하는 데 사용하는 데이터 값을 가져오는 쿼리 기반 구독입니다. 구독이 실행될 때 받는 사람, 보고서 배달 옵션, 렌더링 형식 및 매개 변수 설정에 대한 최신 정보를 가져오기 위한 쿼리가 처리됩니다. 쿼리 결과가 구독 정의에 조합되어 직원 데이터베이스, 고객 데이터베이스 또는 구독자 데이터로 사용할 수 있는 정보가 포함된 기타 데이터베이스에서 이미 유지 관리되고 있는 데이터를 사용하는 동적 구독을 형성합니다.  
  
 새 데이터 기반 구독을 만들거나 기존 구독을 수정 하려면 사용 합니다 **관리** > **구독** 웹 포털에서 페이지입니다. 합니다 **구독** 페이지 만들기 또는 구독을 수정 하는 각 단계를 안내 메시지를 표시 합니다. 구독을 만든 다음 액세스하려면 **내 구독** 페이지나 보고서의 구독 목록을 사용합니다. 데이터 기반 구독을 만드는 방법에 대한 자세한 내용은 [데이터 기반 구독 만들기&#40;SSRS 자습서&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)를 참조하세요.  
  
 이 문서의 내용  
  
-   [데이터 기반 구독 관리 및 삭제](#bkmk_manage_and_delete)  
  
-   [데이터 기반 구독 만들기 및 수정](#bkmk_create_and_modify)  
  
-   [구독 정보를 검색하는 쿼리 정의](#bkmk_define_query)  
  
-   [구독 실행](#bkmk_run_subscription)  
  
##  <a name="bkmk_manage_and_delete"></a> 데이터 기반 구독 관리 및 삭제  
 진행 중인 데이터 기반 구독을 중지 하거나 웹 포털에서 삭제할 수 있습니다. 그러므로 공유 일정을 사용하여 데이터 기반 구독을 트리거하는 것이 좋습니다. 구독이 일시적으로 처리되지 않도록 하려는 경우 이 방법을 사용하면 구독을 트리거하는 일정을 일시 중지할 수 있습니다. 자세한 내용은 [기본 모드 보고서 서버 구독 만들기 및 관리](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)를 참조하세요.  
  
 데이터 기반 구독을 삭제 하려면에서 보고서 옆의 확인란을 선택 합니다 **구독** 페이지를 선택한 후 **삭제**합니다.  
  
 데이터 기반 구독을 취소하는 방법에 대한 자세한 내용은 [실행 중인 프로세스 관리](../../reporting-services/subscriptions/manage-a-running-process.md)를 참조하세요.  
  
##  <a name="bkmk_create_and_modify"></a> 데이터 기반 구독 만들기 및 수정  
 데이터 기반 구독을 만들려면 저장된 자격 증명을 사용하거나 자격 증명을 사용하지 않는 보고서를 선택합니다. 데이터 기반 구독을 만들 때는 표준 구독과 데이터 기반 구독을 쉽게 구분할 수 있도록 설명 필드에 명명 규칙을 사용할 수도 있습니다.  
  
### <a name="to-create-a-data-driven-subscription-native-mode"></a>데이터 기반 구독을 만들려면(기본 모드)  
  
1. 웹 포털에서 보고서가 포함 된 폴더로 이동, 보고서를 마우스 오른쪽 단추로 클릭 하 고 선택 **관리** 드롭다운 메뉴에서.  
  
2. **구독** 탭을 선택합니다.  
  
3. 선택 **+ 새 구독** 에 **구독** 페이지입니다.  
  
### <a name="to-create-a-data-driven-subscription-sharepoint-mode"></a>데이터 기반 구독을 만들려면(SharePoint 모드)  
  
1. SharePoint 문서 라이브러리에서 해당 보고서에 마우스 포인터를 놓고 옵션 메뉴를 연 다음 **구독 관리**를 클릭합니다.  
  
2. **데이터 기반 구독 추가**를 클릭합니다.  
  
### <a name="to-modify-an-existing-data-driven-subscription-native-mode"></a>기존 데이터 기반 구독을 수정하려면(기본 모드)  
  
1. 웹 포털에서 보고서가 포함 된 폴더로 이동, 보고서를 마우스 오른쪽 단추로 클릭 하 고 선택 **관리** 드롭다운 메뉴에서.  
  
2. **구독** 탭을 선택합니다.  
  
3. 수정 하 고 선택 하려면 구독 옆의 확인란을 선택 **편집**합니다. 데이터 기반 구독에 포함 됩니다는 값 "데이터 기반"를 **형식** 열입니다.  
  
### <a name="to-modify-an-existing-data-driven-subscription-sharepoint-mode"></a>기존 데이터 기반 구독을 수정하려면(SharePoint 모드)  
  
1.  SharePoint 문서 라이브러리에서 해당 보고서에 마우스 포인터를 놓고 옵션 메뉴를 연 다음 **구독 관리**를 클릭합니다.  
  
2.  수정할 구독을 선택합니다.  
  
    > [!NOTE]  
    > 이미 지정된 값을 수정할 수 있습니다. 구독자 데이터 저장소에 액세스하는 데 사용되는 암호를 제외한 모든 값은 처음에 만든 대로 표시됩니다. 두 번째 페이지나 다음 페이지에서 값을 수정할 때마다 암호를 다시 입력해야 합니다.  
  
  데이터 기반 구독을 만들려면 먼저 다음 요구 사항을 충족해야 합니다.  
  
-   **보고서 요구 사항**. 보고서는 런타임에 데이터를 검색하기 위해 저장된 자격 증명을 사용하거나 자격 증명을 사용하지 말아야 합니다. 가장 또는 위임된 자격 증명을 사용하여 외부 데이터 원본에 연결하는 보고서는 구독할 수 없습니다. 구독을 만들거나 소유하는 사용자의 자격 증명은 구독이 처리될 때 사용할 수 없습니다. 저장된 자격 증명은 Windows 계정이거나 데이터베이스 사용자 계정일 수 있습니다. 자세한 내용은 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)을 참조하세요.  
  
     모델을 데이터 원본으로 사용하고 모델에 모델 항목 보안 설정이 포함된 경우 보고서 작성기 보고서를 구독할 수 없습니다. 모델 항목 보안을 사용하는 보고서만 이러한 제한을 받습니다.  
  
     `User!UserID` 식이 포함된 보고서에서 데이터 기반 구독을 만들 수 없습니다.  
  
-   **데이터 요구 사항**. 구독자 데이터를 포함하는 액세스 가능한 외부 데이터 원본이 있어야 합니다.  
  
-   **사용자 요구 사항**. 구독 작성자는 "보고서 관리" 및 "모든 구독 관리"의 권한을 갖고 있어야 합니다. 항목 수준의 태스크 사용 권한에 대한 자세한 내용은 [태스크 및 사용 권한](../../reporting-services/security/tasks-and-permissions.md)을 참조하세요. 또한 작성자는 구독자 데이터가 포함된 외부 데이터 원본 액세스를 위해 필요한 자격 증명도 갖고 있어야 합니다.  
  
##  <a name="bkmk_define_query"></a> 구독 정보를 검색하는 쿼리 정의  
 데이터 기반 구독은 구독자 데이터를 검색하는 쿼리나 명령을 지정해야 합니다. 쿼리는 구독자마다 하나의 행을 생성해야 합니다. 전자 메일 배달 확장 프로그램을 사용하는 경우 쿼리는 각 구독자에 대한 유효한 전자 메일 별칭을 반환해야 합니다. 생성되는 배달 수는 쿼리에서 반환하는 행 수에 따라 다릅니다. 행 집합이 10,000개의 행으로 구성되는 경우 구독은 10,000개의 보고서를 배달합니다.  
  
 쿼리를 실행하는 데 시간이 많이 걸리는 경우 추가 처리를 수행할 수 있도록 시간 제한 값을 늘릴 수 있습니다.  
  
 이 단계를 계속하려면 먼저 쿼리의 유효성을 검사해야 합니다. 유효성 검사에서는 쿼리를 처리하지 않지만 다음 선택에서 열을 참조할 수 있도록 행 집합에 있는 모든 열 목록을 반환합니다. 쿼리 유효성 검사에 실패하면 작업을 계속할 수 없습니다. 쿼리 구문이 올바르지 않거나 데이터 원본에 대한 연결이 유효하지 않으면 쿼리의 유효성을 검사하지 못합니다. 데이터 원본을 수정하려면 **뒤로** 단추를 사용합니다.  
  
##  <a name="bkmk_run_subscription"></a> 구독 실행  
 구독의 처리 조건을 지정해야 합니다. 일정을 지정하거나 보고서 실행 스냅샷 업데이트에 맞춰 구독을 실행할 수 있습니다. 데이터 기반 구독 처리 방법은 표준 구독 처리 방법과 동일합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [기본 모드 보고서 서버 구독 만들기 및 관리](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)   
 [구독 및 배달&#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [보고서 서버의 웹 포털(SSRS 기본 모드)](../../reporting-services/web-portal-ssrs-native-mode.md)   
 [기본 모드 보고서 서버 구독 만들기 및 관리](create-and-manage-subscriptions-for-native-mode-report-servers.md)   
 [구독 사용 (웹 포털)](../../reporting-services/working-with-subscriptions-web-portal.md) [내 구독 사용 (기본 모드 보고서 서버)](../../reporting-services/subscriptions/use-my-subscriptions-native-mode-report-server.md)  
 