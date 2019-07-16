---
title: 도메인 간 규칙 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.dm.testcdrule.f1
- sql13.dqs.dm.cdrules.f1
ms.assetid: 0f3f5ba4-cc47-4d66-866e-371a042d1f21
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 45222a4ae99578c40ce14870433fb929c1127f51
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992335"
---
# <a name="create-a-cross-domain-rule"></a>도메인 간 규칙 만들기

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  이 항목에서는 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )의 기술 자료에서 복합 도메인의 도메인 간 규칙을 만드는 방법에 대해 설명합니다. 도메인 간 규칙은 복합 도메인에 포함된 단일 도메인에서 값 사이의 관계를 테스트합니다. 도메인 값이 정확하고 비즈니스 요구 사항에 맞는 것으로 간주되려면 도메인 간 규칙이 복합 도메인 전체에서 유효해야 합니다. 도메인 간 규칙은 도메인 값의 유효성 검사, 수정 및 표준화에 사용됩니다.  
  
 도메인 간 규칙의 If 절과 Then 절은 각각 복합 도메인의 단일 도메인 중 하나에 대해 정의됩니다. 각 절은 서로 다른 단일 도메인에 대해 정의되어야 합니다. 도메인 간 규칙은 여러 개의 단일 도메인과 관련되어야 합니다. 복합 도메인에 단순 도메인 규칙(단일 도메인 전용)을 정의할 수는 없습니다. 단일 도메인에 도메인 규칙을 정의하여 이 작업을 수행합니다. If 절과 Then 절은 각각 하나 이상의 조건을 포함할 수 있습니다.  
  
 결정적 조건이 있는 도메인 간 규칙은 조건 값의 동의어와 값 자체에 규칙 논리를 적용합니다. If 절과 Then 절의 결정적 조건은 값이 다음 값과 같음, 값이 다음 값과 같지 않음, 값이 다음에 속함 또는 값이 다음에 포함되지 않음입니다. 예를 들어, 복합 도메인에 대 한 다음 도메인 간 규칙이 있다고 가정 합니다. "'City'의 경우 값이 'Los Angeles'와 같으면 'State'의 경우 값은 'CA'와 같습니다. ‘Los Angeles’와 ‘LA’가 동의어인 경우 이 규칙은 ‘Los Angeles CA’와 ‘LA CA’에 대해 올바른 결과를, ‘Los Angeles WA’ 및 ‘LA WA’에 대해서는 오류를 반환합니다.  
  
 도메인 간 규칙 *값이 다음 값과 같음* 에서 결정적 **Then**절은 도메인 간 규칙의 유효성에 대해 알려줄 뿐만 아니라 데이터 정리 작업 시 데이터를 수정합니다. 자세한 내용은 [Data Correction using Definitive Cross-Domain Rules](../data-quality-services/cleanse-data-in-a-composite-domain.md#CDCorrection) 에서 [Cleanse Data in a Composite Domain](../data-quality-services/cleanse-data-in-a-composite-domain.md)를 참조하세요.  
  
 단일 도메인에만 영향을 주는 모든 단순한 규칙 뒤에서 도메인 간 규칙을 사용하세요. 값이 단일 도메인 규칙(존재할 경우)을 전달할 경우에만 도메인 간 규칙이 적용됩니다. 먼저 규칙이 실행되는 복합 도메인과 단일 도메인을 모두 정의해야 규칙을 실행할 수 있습니다.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
 도메인 간 규칙을 만들려면 복합 도메인을 만들어 열어 놓아야 합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 도메인 간 규칙을 만들려면 DQS_MAIN 데이터베이스의 dqs_kb_editor 또는 dqs_administrator 역할이 있어야 합니다.  
  
##  <a name="Create"></a> 도메인 간 규칙 만들기  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Data Quality Client 응용 프로그램을 실행합니다](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면에서 기술 자료를 열거나 만듭니다. **도메인 관리** 를 작업으로 선택한 다음 **열기** 또는 **만들기**를 클릭합니다. 자세한 내용은 [기술 자료 만들기](../data-quality-services/create-a-knowledge-base.md) 또는 [기술 자료 열기](../data-quality-services/open-a-knowledge-base.md)를 참조하세요.  
  
    > [!NOTE]  
    >  도메인 관리는 별도의 도메인 관리 작업을 위한 5개 탭이 포함된 Data Quality Services 클라이언트의 페이지에서 수행됩니다. 도메인 관리는 마법사 기반 프로세스가 아닙니다. 모든 관리 작업은 별도로 수행할 수 있습니다.  
  
3.  **도메인 관리** 페이지의 **도메인 목록** 에서 도메인 규칙을 만들 복합 도메인을 선택하거나 새 복합 도메인을 만듭니다. 새 도메인을 만들어야 하는 경우 [Create a Composite Domain](../data-quality-services/create-a-composite-domain.md)를 참조하세요.  
  
4.  **CD 규칙** 탭을 클릭합니다.  
  
5.  **새 도메인 규칙을 추가합니다.** 를 클릭하고 규칙의 이름과 설명을 입력합니다.  
  
6.  **활성** 을 선택하여 해당 규칙이 실행되도록 지정하거나(기본값) 선택 취소하여 규칙이 실행되지 않도록 합니다.  
  
7.  다음과 같이 If 절을 만듭니다.  
  
    1.  If 절 창의 도메인 목록에서 복합 도메인에 포함된 단일 도메인 중 하나를 if 절의 주체로 선택합니다. 복합 도메인에서 임의의 단일 도메인을 선택할 수 있습니다.  
  
    2.  절의 첫째 조건에 대한 드롭다운 목록에서 조건을 선택합니다.  
  
    3.  조건에 값이 필요한 경우 조건과 연결된 입력란에 값을 입력합니다.  
  
    4.  if 절에 다른 조건이 필요한 경우 **선택한 절에 새 조건을 추가합니다.** 를 클릭합니다. 연산자를 선택하고 조건을 선택한 후 필요하면 조건의 값을 입력합니다.  
  
    5.  조건 순서를 변경하려면 조건의 왼쪽을 클릭하여 조건을 선택하고 위쪽 화살표나 아래쪽 화살표를 클릭합니다.  
  
    6.  조건을 숨기려면 도메인 이름 왼쪽의 빼기 기호를 클릭합니다. 조건을 표시하려면 더하기 기호를 클릭합니다.  
  
8.  Then 절 창의 도메인 목록에서 if 절의 주체 외에 단일 도메인을 선택하여 Then 절을 만듭니다. 그런 다음 if 절을 만들 때와 동일한 단계를 사용하여 Then 절을 작성합니다.  
  
9. 다음 테스트 절차를 진행합니다.  
  
##  <a name="Test"></a> 도메인 간 규칙 테스트  
  
1.  도메인 간 규칙을 다음과 같이 테스트합니다.  
  
    1.  복합 도메인 창의 오른쪽 위 모퉁이에서 **테스트 데이터에서 선택한 도메인 규칙 실행** 아이콘을 클릭합니다.  
  
    2.  **도메인 규칙 테스트** 대화 상자에서 **도메인 규칙에서 새 테스트 용어를 추가합니다.** 아이콘을 클릭합니다.  
  
    3.  If 절과 연결된 단일 도메인 및 Then 절과 연결된 단일 도메인에 대해 테스트 값을 입력합니다. If 절에 입력한 테스트 값은 해당 절의 조건과 일치해야 합니다. 그렇지 않으면 **유효성 검사** 열에 물음표가 입력되어 도메인 간 규칙이 테스트 데이터에 적용되지 않음을 나타냅니다.  
  
    4.  **도메인 규칙에서 새 테스트 용어를 추가합니다.** 아이콘을 다시 클릭하여 다른 테스트 값 집합을 추가합니다.  
  
    5.  **모든 용어에 대해 도메인 규칙 테스트** 아이콘을 클릭합니다. 테스트 값 집합이 유효하면 행의 **유효성 검사** 열에 확인 표시가 입력되고 테스트 값 집합이 유효하지 않으면 행의 유효성 검사 열에 느낌표가 있는 삼각형이 입력됩니다.  
  
    6.  테스트 완료 후 **복합 도메인 규칙 테스트** 대화 상자에서 **닫기** 를 클릭합니다.  
  
2.  도메인 간 규칙을 완성하면 **End the Domain Management Activity** 에서 설명한 대로 [마침](https://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0)을 클릭하여 도메인 관리 작업을 완료합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: 도메인 간 규칙을 만든 후  
 도메인 간 규칙을 만든 후 도메인에 대해 다른 도메인 관리 태스크를 수행하거나, 기술 자료 검색을 수행하여 도메인에 정보를 추가하거나, 도메인에 일치 정책을 추가할 수 있습니다. 자세한 내용은 [기술 자료 검색 수행](../data-quality-services/perform-knowledge-discovery.md), [도메인 관리](../data-quality-services/managing-a-domain.md) 또는 [일치 정책 만들기](../data-quality-services/create-a-matching-policy.md)를 참조하세요.  
  
  
