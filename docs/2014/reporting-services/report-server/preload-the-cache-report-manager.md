---
title: 캐시 사전 로드(보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- cache [Reporting Services]
- preloading cache
ms.assetid: 152a1051-8aa5-4c01-bc85-f8be8971b0cd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 98ce4f723c0b4c04b166b01d17e8014567253518
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66103591"
---
# <a name="preload-the-cache-report-manager"></a>캐시 사전 로드(보고서 관리자)
  공유 데이터 세트에 대한 캐시 새로 고침 계획을 만들어 공유 데이터 세트에 대한 캐시를 미리 로드할 수 있습니다.  
  
 다음과 같은 두 가지 방법으로 보고서에 대한 캐시를 미리 로드할 수 있습니다.  
  
1.  보고서에 대한 캐시 새로 고침 계획을 만듭니다. 이는 선호되는 방법입니다.  
  
2.  데이터 기반 구독을 사용하여 매개 변수가 있는 보고서 인스턴스와 함께 캐시를 미리 로드할 수 있습니다. 이것이 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 이전의 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]버전에서 캐시를 미리 로드할 수 있는 유일한 방법이었습니다. 자세한 내용은 [보고서 캐시&#40;SSRS&#41;](caching-reports-ssrs.md)버전에서 캐시를 미리 로드할 수 있는 유일한 방법이었습니다.  
  
 보고서 또는 공유 데이터 세트를 캐시하려면 먼저 다음 조건을 충족해야 합니다.  
  
-   공유 데이터 세트 또는 보고서에 캐싱이 설정되어 있어야 합니다.  
  
-   공유 데이터 세트 또는 보고서에 대한 공유 데이터 원본이 저장된 자격 증명을 사용하거나 자격 증명을 사용하지 않도록 구성되어 있어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 실행되고 있어야 합니다.  
  
### <a name="to-preload-the-cache-by-creating-a-cache-refresh-plan"></a>캐시 새로 고침 계획을 만들어 캐시를 미리 로드하려면  
  
1.  [보고서 관리자&#40;SSRS 기본 모드&#41;](../report-manager-ssrs-native-mode.md)를 시작합니다.  
  
2.  보고서 관리자에서 **내용** 페이지로 이동한 다음 캐시할 항목으로 이동합니다.  
  
3.  항목을 마우스로 가리키고 드롭다운 목록을 클릭한 다음 **관리**를 클릭합니다.  
  
4.  **캐시 새로 고침 옵션** 탭을 클릭합니다.  
  
5.  도구 모음에서 **새 캐시 새로 고침 계획**을 클릭합니다.  
  
    > [!NOTE]  
    >  항목에 캐싱이 설정되어 있지 않으면 캐싱을 설정하라는 메시지가 표시됩니다. 캐싱을 설정하려면 **확인**을 클릭합니다.  
  
     캐시 새로 고침 계획 페이지가 열립니다.  
  
6.  새로 고침 계획에 대한 설명을 입력할 수도 있습니다.  
  
7.  공유 일정의 경우 **공유 일정**을 클릭한 다음 사용할 일정의 이름을 선택합니다.  
  
     사용자 지정 일정의 경우 **항목별 일정**을 클릭한 다음 **구성**을 클릭합니다.  
  
8.  일정을 구성합니다.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-preload-the-cache-with-a-user-specific-report-by-using-a-data-driven-subscription"></a>데이터 기반 구독을 사용하여 사용자별 보고서와 함께 캐시를 미리 로드하려면  
  
1.  [보고서 관리자&#40;SSRS 기본 모드&#41;](../report-manager-ssrs-native-mode.md)를 시작합니다.  
  
2.  보고서 관리자에서 **내용** 페이지로 이동한 후 구독을 만들 보고서로 이동합니다.  
  
3.  보고서를 클릭하고 **구독** 탭을 클릭한 다음 **새 데이터 기반 구독**을 클릭합니다.  
  
4.  구독에 대한 설명을 입력합니다(옵션).  
  
5.  **받은 사람에게 알림을 보내는 방법 지정** 목록에서 **Null 배달 공급자**를 선택합니다.  
  
6.  데이터 원본 유형을 지정한 후 **다음** 을 클릭하여 데이터 원본을 구성합니다.  
  
7.  구독자 데이터를 포함하는 데이터 원본에 액세스하기 위한 연결 형식, 연결 문자열 및 자격 증명을 지정합니다. 다음 예에서는 Subscribers라는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 데 사용되는 연결 문자열을 보여 줍니다.  
  
    ```  
    data source=<servername>; initial catalog=Subscribers  
    ```  
  
8.  **다음**을 클릭합니다.  
  
9. 구독자 데이터를 검색하는 쿼리나 명령을 지정합니다. 처리하는 데 시간이 오래 걸리는 쿼리에 대해 제한 시간 값을 늘립니다(옵션). 예를 들어:  
  
    ```  
    Select * from UserInfo  
    ```  
  
10. **유효성 검사**를 클릭합니다. 계속하기 전에 쿼리의 유효성을 검사해야 합니다. **쿼리의 유효성을 검사했습니다** 메시지가 나타나면 **다음**을 클릭합니다.  
  
11. Null 배달 공급자에 대한 배달 확장 프로그램 설정을 구성할 수 없으므로 **다음**을 클릭합니다.  
  
12. 구독에 대해 보고서 매개 변수 값을 지정하고 **다음**을 클릭합니다.  
  
13. 구독 처리 시기를 지정합니다. **보고서 서버에서 보고서 데이터가 업데이트될 때**는 선택하지 마십시오. 이 설정은 스냅샷에만 사용할 수 있습니다. 기존 일정을 사용하려면 **공유 일정**을 선택합니다.  
  
     그렇지 않고 사용자 지정 일정을 만들려면 **이 구독에 대해 생성된 일정** 을 클릭한 후 **다음**을 클릭합니다. 일정을 구성하고 **마침**을 클릭합니다.  
  
    > [!NOTE]  
    >  구독자가 최신 보고서를 받도록 하려면 구성하는 일정이 구독자에 대해 정의한 보고서 배달 일정과 일치해야 합니다. 자세한 내용은 [보고서 관리자&#40;SSRS 기본 모드&#41;](../report-manager-ssrs-native-mode.md)를 참조하세요.  
  
14. 다음과 같이 보고서에 대한 실행 옵션을 구성합니다. 보고서 페이지에서 **속성** 탭을 클릭합니다.  
  
15. 왼쪽 프레임에서 **실행** 탭을 클릭합니다.  
  
16. 해당 페이지에서 **가장 최근 데이터로 이 보고서 렌더링**을 선택합니다.  
  
17. 다음 두 캐시 옵션 중에서 하나를 선택하고 만료 시간을 구성합니다.  
  
    -   캐시된 복사본이 특정 시간 후에 만료되도록 하려면 **보고서의 임시 복사본을 캐시합니다. 보고서 복사본은 다음 분 후에 만료됩니다.** 를 클릭합니다. 보고서 만료 시간(분)을 입력합니다.  
  
    -   일정에 따라 캐시된 복사본이 만료되도록 하려면 **보고서의 임시 복사본을 캐시합니다. 보고서 복사본은 다음 일정으로 만료됩니다.** 를 클릭합니다. 를 클릭합니다. **구성**을 클릭하거나 공유 일정을 선택하여 보고서 만료 일정을 설정합니다.  
  
18. **적용**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Data-Driven Subscriptions](../subscriptions/data-driven-subscriptions.md)   
 [데이터 기반 구독 만들기&#40;SSRS 자습서&#41;](../create-a-data-driven-subscription-ssrs-tutorial.md)   
 [성능, 스냅숏, 캐싱 &#40;Reporting Services&#41;](performance-snapshots-caching-reporting-services.md)   
 [보고서 처리 속성 설정](set-report-processing-properties.md)   
 [보고서 캐시&#40;SSRS&#41;](caching-reports-ssrs.md)  
  
  
