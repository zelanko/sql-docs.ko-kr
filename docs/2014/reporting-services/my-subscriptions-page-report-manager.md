---
title: 내 구독 페이지 (보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 491a85a3-f323-4155-a0a8-de2779899995
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 29824d30b1fdd96c2bc847b8908b49340a05aaf3
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56026904"
---
# <a name="my-subscriptions-page-report-manager"></a>내 구독 페이지(보고서 관리자)
  내 구독 페이지를 사용하여 모든 구독을 한 곳에서 확인할 수 있습니다. 이 페이지에서는 소유한 모든 구독을 액세스하고 수정 또는 삭제할 수 있습니다. 사용자는 자신이 만든 구독만 소유합니다. 다른 사용자가 정의한 구독에는 액세스할 수 없을 뿐 아니라 사용하지만 소유하지 않는 구독(예: 다른 사용자가 정의한 기존 구독에 자신의 이름이 추가된 경우)에도 액세스할 수 없습니다. 이 페이지에서 구독을 만들 수는 없습니다. 구독을 만드는 방법에 대 한 자세한 내용은 참조는 [새 구독 또는 구독 편집 페이지 &#40;보고서 관리자&#41;](../../2014/reporting-services/new-subscription-or-edit-subscription-page-report-manager.md)합니다.  
  
 기본적으로 구독은 보고서 이름을 기준으로 사전순으로 정렬됩니다. 구독 정렬 방법을 변경하려면 다른 열 머리글을 클릭합니다. 구독이 없거나 구독 생성 또는 관리 권한이 해제되어 있는 경우에는 이 페이지에 구독이 표시되지 않습니다.  
  
> [!NOTE]  
>  이 기능은 일부 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]버전에서는 사용할 수 없습니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 참조 하세요 [SQL Server 2014 버전에서 지 원하는 기능](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다.  
  
## <a name="navigation"></a>탐색  
 사용자 인터페이스(UI)에서 이 위치를 탐색하려면 다음 절차를 사용하십시오.  
  
### <a name="to-open-the-my-subscriptions-page"></a>내 구독 페이지를 열려면  
  
1.  보고서 관리자를 엽니다.  
  
2.  페이지 맨 위에서 오른쪽 모퉁이에 있는 내 구독을 클릭합니다.  
  
    > [!NOTE]  
    >  구독 만들기 권한이 없는 경우에도 항상 내 구독을 사용할 수 있습니다.  
  
## <a name="options"></a>변수  
 **Delete**  
 삭제할 각 구독 옆에 있는 확인란을 선택한 다음 **삭제**를 클릭합니다.  
  
 **편집**  
 설명을 보거나 편집하려면 클릭합니다.  
  
 **보고서**  
 구독에 지정된 보고서를 표시합니다. 보고서를 보려면 보고서 이름을 클릭합니다.  
  
 **설명**  
 보고서에 대한 설명을 표시합니다. 보고서의 구독 정보를 보거나 편집하려면 설명을 클릭합니다.  
  
 **Folder**  
 구독에 지정된 보고서를 포함하는 폴더를 표시합니다. 폴더의 내용을 보려면 폴더 이름을 클릭합니다.  
  
 **트리거**  
 구독을 실행하는 조건을 식별합니다. **TimedSubscription** 트리거는 구독이 실행되는 시기를 정의하는 일정을 기반으로 합니다. **SnapshotUpdated** 트리거는 보고서 스냅숏에 대한 업데이트를 기반으로 합니다.  
  
 **마지막 실행**  
 구독이 마지막으로 처리된 시간을 표시합니다.  
  
 **상태**  
 구독 상태를 표시합니다. 일반적으로 상태 값은 "신규" 또는 구독이 마지막으로 실행된 날짜 및 시간입니다.  
  
 "잘못된 데이터" 상태 값은 더 이상 유효하지 않은 암호화된 값, 즉 보고서를 실행하는 데 사용되는 저장된 자격 증명에 대한 포인터가 구독에 포함되어 있는 경우 발생합니다. 데이터를 암호화 및 해독하는 데 사용되는 대칭 키를 보고서 서버에서 다시 만들면 기존의 암호화된 값은 사용할 수 없게 됩니다.  
  
 비활성화된 구독은 처리할 수 없습니다. 구독을 업데이트하고 작동시키려면 해당 구독을 열어서 저장합니다.  
  
## <a name="see-also"></a>관련 항목  
 [구독 및 배달&#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [보고서 관리자 F1 도움말](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
