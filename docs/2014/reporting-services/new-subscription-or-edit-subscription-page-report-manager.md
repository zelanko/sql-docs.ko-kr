---
title: 새 구독 또는 구독 편집 페이지 (보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: e02d6529-ce67-4305-b7f0-433997e99c21
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 968362b2835c0e76f2a44c44e6cd427af863e8e4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108136"
---
# <a name="new-subscription-or-edit-subscription-page-report-manager"></a>새 구독 또는 구독 편집 페이지(보고서 관리자)
  새 구독 또는 구독 편집 페이지를 사용하여 보고서에 대한 새 구독을 만들거나 기존 구독을 수정할 수 있습니다. 이 페이지의 옵션은 사용자의 역할 할당에 따라 다릅니다. 고급 권한이 있는 사용자는 추가 옵션으로 작업할 수 있습니다.  
  
 구독은 무인 모드로 실행될 수 있는 보고서에 대해 지원됩니다. 이 보고서는 저장된 자격 증명을 사용하거나 자격 증명을 사용하지 않아야 합니다. 보고서에서 매개 변수를 사용하는 경우에는 기본값을 지정해야 합니다. 보고서 실행 설정을 변경하거나 매개 변수 속성에서 사용하는 기본값을 제거하면 구독이 비활성 상태로 바뀔 수 있습니다. 자세한 내용은 [기본 모드 보고서 서버 구독 만들기 및 관리](../../2014/reporting-services/create-manage-subscriptions-native-mode-report-servers.md)합니다.  
  
> [!NOTE]  
>  이 기능은 일부 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]버전에서는 사용할 수 없습니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 참조 하세요 [SQL Server 2014 버전에서 지 원하는 기능](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다.  
  
## <a name="navigation"></a>탐색  
 사용자 인터페이스(UI)에서 이 위치를 탐색하려면 다음 절차를 사용하십시오.  
  
### <a name="to-open-the-new-subscription-or-edit-subscription-page"></a>새 구독 또는 구독 편집 페이지를 열려면  
  
1.  보고서 관리자를 열고 구독을 추가할 보고서를 찾습니다.  
  
2.  보고서 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
3.  드롭다운 메뉴에서 다음 중 하나를 수행하십시오.  
  
    -   **관리**를 클릭합니다. 보고서의 일반 속성 페이지가 열립니다. **구독** 탭을 선택합니다. 도구 모음에서 **새 구독**을 클릭하거나 기존 구독을 선택하고 **편집**을 클릭합니다.  
  
    -   **구독**을 클릭합니다. 보고서의 **새 구독** 페이지가 열립니다.  
  
## <a name="options"></a>변수  
 **배달 방법**  
 보고서를 배포하는 데 사용할 배달 확장 프로그램을 선택합니다. 선택한 배달 확장 프로그램에 따라 다음 설정이 표시됩니다.  
  
-   전자 메일 구독에서는 전자 메일 사용자에게 익숙한 필드(예: **받는 사람**, **제목**및 **우선 순위** 필드)를 제공합니다. 보고서를 포함시키거나 첨부하려면 **보고서 포함** 을 지정하고 보고서에 대한 URL을 포함시키려면 **링크 포함** 을 지정합니다. 첨부 또는 포함된 보고서의 표시 형식을 선택하려면 **렌더링 형식** 을 지정합니다.  
  
-   파일 공유 구독은 대상 위치를 지정할 수 있도록 허용하는 필드를 제공합니다. 모든 보고서를 파일 공유로 배달할 수 있습니다. 그러나 대화형 기능을 지원하는 보고서(관련 행 및 열에 대한 드릴다운을 지원하는 행렬 보고서 포함)는 정적 파일로 렌더링됩니다. 드릴다운 행 및 열은 정적 파일에서 볼 수 없습니다. 파일 공유 이름 명명 규칙 (UNC (Uniform) 형식으로 지정 해야 합니다 (예를 들어 \\\mycomputer\public\myreportfiles). 경로 이름 뒤에 백슬래시를 사용하지 마십시오. 보고서 파일은 렌더링 형식을 기반으로 하는 파일 형식으로 배달됩니다. 예를 들어 **Excel**을 선택할 경우 보고서는 .xls 파일로 배달됩니다.  
  
 배달 확장 프로그램의 가용성은 보고서 서버에 설치 및 구성되었는지 여부에 따라 다릅니다. 보고서 서버 전자 메일은 기본 배달 확장 프로그램이지만 먼저 구성을 해야 사용할 수 있습니다. 파일 공유 배달은 구성이 필요하지 않지만 먼저 공유 폴더를 정의해야 사용할 수 있습니다.  
  
## <a name="subscription-processing-options"></a>구독 처리 옵션  
 구독 처리 조건을 정의하려면 이 설정을 사용합니다. 일부 옵션은 매개 변수를 사용하는 보고서나 보고서 실행 스냅샷으로 실행되는 보고서에서만 사용할 수 있습니다.  
  
 **보고서 내용은 새로 고칠 때**  
 일정에 따라 새로 고쳐지는 보고서 스냅샷을 구독하려면 이 옵션을 선택합니다. 이 옵션은 보고서 실행 스냅샷으로 실행되는 보고서를 구독하는 경우에만 표시됩니다. 보고서 실행 스냅샷의 내용은 일반적으로 일정에 따라 새로 고쳐집니다. 이 모드로 실행되는 보고서의 경우 스냅샷을 새로 고쳤을 때 발생하도록 구독을 정의할 수 있습니다.  
  
 **예약된 된 보고서 실행이 완료 되었을 때**  
 구독이 처리되는 시기를 결정하는 일정을 만듭니다.  
  
 **공유 일정**  
 구독을 처리할 미리 정의된 일정을 선택합니다.  
  
 **매개 변수 값 입력**  
 매개 변수 있는 보고서를 구독할 경우 이 옵션을 사용합니다. 이 옵션은 매개 변수가 있는 보고서에서만 사용할 수 있습니다. 매개 변수가 있는 보고서를 구독할 경우 구독을 통해 배달되는 보고서 버전을 만드는 데 필요한 매개 변수 값을 지정할 수 있습니다. 예를 들어 지역 코드를 지정하여 특정 지역의 판매 데이터를 선택할 수 있습니다. 값을 지정하지 않으면 기본값이 사용됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [전자 메일 배달을 위한 보고서 서버 구성 &#40;SSRS 구성 관리자&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)   
 [보고서 관리자&#40;SSRS 기본 모드&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [일정 만들기, 수정 및 삭제](subscriptions/create-modify-and-delete-schedules.md)   
 [보고서 관리자 F1 도움말](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
