---
title: 구독 페이지 (보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cf3a6bd0-e0b2-4875-a532-63ef34cfa860
caps.latest.revision: 27
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 6b6a3befb6794327af0fd5fa2ef92a48b67529a5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090804"
---
# <a name="subscriptions-page-report-manager"></a>구독 페이지(보고서 관리자)
  구독 페이지를 사용하여 현재 보고서나 공유 데이터 원본의 구독을 모두 나열할 수 있습니다. 모든 구독 태스크 관리가 뜻하는 바와 같이 충분한 권한이 있으면 모든 사용자의 구독을 볼 수 있습니다. 그렇지 않으면 이 페이지는 사용자가 소유하는 구독만 표시합니다.  
  
> [!NOTE]  
>  다른 페이지에서도 구독 정보를 포함할 수 있습니다. 자세한 내용은 참조 [내 구독 페이지 &#40;보고서 관리자&#41; ](../../2014/reporting-services/my-subscriptions-page-report-manager.md) 한 곳에서 모든 구독에 액세스 하려면 또는 [새 구독 또는 구독 편집 페이지 &#40;보고서 관리자&#41; ](../../2014/reporting-services/new-subscription-or-edit-subscription-page-report-manager.md) 만들거나 구독을 편집 합니다.  
  
 일부 옵션은 작업할 기존 구독이 있는 경우에만 표시됩니다. 정의된 구독이 없는 경우 보고서에서 이 페이지를 액세스하면 페이지에 **새 구독** 및 **새 데이터 기반 구독** 옵션만 표시됩니다.  
  
 새 구독을 만들기 전에 보고서 데이터 원본에서 저장된 자격 증명을 사용하는지 확인해야 합니다. 자격 증명을 저장하려면 데이터 원본 속성 페이지를 사용하십시오. 자세한 내용은 참조 [데이터 원본 속성 페이지 &#40;보고서 관리자&#41;](../../2014/reporting-services/data-sources-properties-page-report-manager.md)합니다.  
  
> [!NOTE]  
>  이 기능은 일부 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]버전에서는 사용할 수 없습니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], 참조 [SQL Server 2014 버전에서 지 원하는 기능](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다.  
  
## <a name="navigation"></a>탐색  
 사용자 인터페이스(UI)에서 이 위치를 탐색하려면 다음 절차를 사용하십시오.  
  
### <a name="to-open-the-subscriptions-page-for-report"></a>보고서의 구독 페이지를 열려면  
  
1.  보고서 관리자를 열고 구독을 보거나 구성하려는 보고서를 찾습니다.  
  
2.  보고서 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
3.  드롭다운 메뉴에서 **관리**를 클릭합니다. 보고서의 일반 속성 페이지가 열립니다.  
  
4.  **구독** 탭을 선택합니다.  
  
## <a name="options"></a>변수  
 **Delete**  
 구독을 삭제하려면 클릭합니다. 구독을 삭제하기 전에 삭제할 각 구독 옆의 확인란을 선택하십시오.  
  
 **새 구독**  
 현재 보고서에 대한 새 구독을 만들려면 클릭합니다. 이 단추는 보고서에서 저장된 자격 증명을 사용하는 경우나 자격 증명을 사용하지 않는 경우에 설정됩니다. 공유 데이터 원본에 대한 구독 페이지를 여는 경우에는 이 단추를 사용할 수 없습니다.  
  
 **새 데이터 기반 구독**  
 해당 정보를 포함하는 데이터 저장소에 대한 쿼리나 명령을 통해 구독자 목록과 배달 옵션을 생성하려면 클릭합니다. 이 단추는 보고서에서 저장된 자격 증명을 사용하는 경우나 자격 증명을 사용하지 않는 경우에 설정됩니다. 공유 데이터 원본에 대한 구독 페이지를 여는 경우에는 이 단추를 사용할 수 없습니다.  
  
 **편집**  
 설명을 보거나 편집하려면 클릭합니다.  
  
 **보고서**  
 공유 데이터 원본에서 이 페이지를 열면 이 열은 구독이 정의된 보고서를 식별합니다. **폴더** 열은 보고서 위치를 식별합니다.  
  
 **설명**  
 보고서에 대한 설명을 표시합니다.  
  
 **트리거**  
 구독을 실행하는 조건을 식별합니다. **TimedSubscription** 트리거는 구독이 실행되는 시기를 정의하는 일정을 기반으로 합니다. **SnapshotUpdated** 트리거는 보고서 스냅숏에 대한 업데이트를 기반으로 합니다.  
  
 **소유자**  
 구독을 만든 사용자 이름을 표시합니다.  
  
 **마지막 실행**  
 구독이 마지막으로 처리된 시간을 표시합니다.  
  
 **상태**  
 구독 상태를 표시합니다. 일반적으로 상태 값은 신규 또는 구독이 마지막으로 실행된 날짜 및 시간입니다.  
  
 "잘못된 데이터" 상태 값은 더 이상 유효하지 않은 암호화된 값, 즉 보고서를 실행하는 데 사용되는 저장된 자격 증명에 대한 포인터가 구독에 포함되어 있는 경우 발생합니다. 데이터를 암호화 및 해독하는 데 사용되는 대칭 키를 보고서 서버에서 다시 만들면 기존의 암호화된 값은 사용할 수 없게 됩니다.  
  
 비활성화된 구독은 처리할 수 없습니다. 구독을 업데이트하고 작동시키려면 해당 구독을 열어서 저장합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 관리자 &#40;SSRS 기본 모드&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [만들기, 수정 및 표준 구독을 삭제 &#40;기본 모드의 Reporting Services&#41;](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)   
 [일정 만들기, 수정 및 삭제](subscriptions/create-modify-and-delete-schedules.md)   
 [보고서 관리자 F1 도움말](../../2014/reporting-services/report-manager-f1-help.md)  
  
  