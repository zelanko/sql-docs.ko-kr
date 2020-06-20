---
title: 등록 된 서버를 사용 하 여 요청 시 평가 수행 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: c14034ef-6e0b-4df5-8072-bfb8d90b3172
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: e3ffcef923eaeb3ba48eacaca870bd3355fb6661
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85035580"
---
# <a name="perform-an-on-demand-evaluation-by-using-registered-servers"></a>등록된 서버를 사용하여 요청 시 평가 수행

  등록된 서버를 사용하여 하나 이상의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 대해 최선의 구현 방법 정책의 요청 시 평가를 수행할 수 있습니다. 로컬 서버 그룹 또는 중앙 관리 서버를 사용할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 또는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 이상 버전이 실행되는 서버 그룹 멤버에 대해 최선의 구현 방법 정책의 요청 시 평가를 수행할 수 있습니다. 그러나 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 또는 [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]에서 지원되지 않는 정책에서 참조하는 속성이 있는 경우 예외 오류가 발생할 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 등록된 서버에서 하나 이상의 서버 등록을 구성한 경우에만 이 태스크를 수행할 수 있습니다. 자세한 내용은 아래 항목을 참조하세요.  
  
-   [서버 그룹 만들기 또는 편집&#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
-   [연결 된 서버 &#40;SQL Server Management Studio&#41;등록 ](../ssms/register-servers/register-a-connected-server-sql-server-management-studio.md)합니다.  
  
-   [중앙 관리 서버 및 서버 그룹 만들기&#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)  
  
### <a name="to-evaluate-best-practices-policies-against-a-server-group"></a>서버 그룹에 대해 최선의 구현 방법 정책을 평가하려면  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 **보기** 메뉴에서 **등록된 서버**를 클릭합니다.  
  
2.  **데이터베이스 엔진**를 확장 한 다음 구성에 따라 **로컬 서버 그룹**또는 **중앙 관리 서버**를 확장 합니다.  
  
3.  다음 중 하나를 수행합니다.  
  
    -   로컬 서버 그룹 또는 중앙 관리 서버에서 관리 하는 모든 서버에 대해 정책을 평가 하려면 로컬 서버 그룹 이름 또는 중앙 관리 서버 이름을 마우스 오른쪽 단추로 클릭 한 다음 **정책 평가**를 클릭 합니다.  
  
        > [!NOTE]  
        >  중앙 관리 서버를 통해 정책을 평가하면 중앙 관리 서버 자체에 대해서는 정책이 평가되지 않습니다.  
  
    -   특정 서버나 서버 그룹에 대해 정책을 평가 하려면 **로컬 서버 그룹** 또는 중앙 관리 서버 이름을 확장 하 고 정책을 평가할 서버 또는 서버 그룹을 마우스 오른쪽 단추로 클릭 한 다음 **정책 평가**를 클릭 합니다.  
  
4.  **정책 평가** 대화 상자에서 **원본** 상자 옆의 줄임표 (**...**) 단추를 클릭 합니다.  
  
5.  **원본 선택** 대화 상자에서 평가할 정책 파일의 원본으로 **파일** 또는 **서버** 를 선택할 수 있습니다. **서버**를 클릭 하면 로컬 또는 원격 서버에서 정책 기반 관리로 이전에 가져온 모범 사례 정책에 대 한 요청 시 평가를 수행할 수 있습니다. 이 자습서에서는 **파일**을 클릭 한 다음 평가할 개별 정책 파일을 선택 합니다. 이렇게 하려면 다음 단계를 수행하세요.  
  
    1.  **파일**을 클릭 합니다.  
  
    2.  **파일**옆에 있는 줄임표 (**...**) 단추를 클릭 합니다.  
  
    3.  평가할 하나 이상의 .xml 정책 파일을 선택 하 고 **열기**를 클릭 합니다.  
  
         선택한 파일의 목록이 **파일** 상자에 나타납니다.  
  
    4.  **원본 선택** 대화 상자에서 **확인**을 클릭 합니다.  
  
    5.  **정책 로드 중** 대화 상자가 나타나면 **닫기**를 클릭 합니다.  
  
     선택한 정책이 **정책 선택** 페이지에 나열 됩니다. 정책 옆의 경고 아이콘은 정책에 스크립트가 포함되어 있다는 것을 나타냅니다.  
  
6.  **평가** 를 클릭 하 여 정책을 평가 합니다.  
  
7.  일부 정책 실패의 경우 정책 기반 관리를 사용하면 대상에서 정책 준수를 즉시 강제할 수 있습니다. 이러한 실패의 경우 실패한 정책 옆에 확인란이 나타납니다. 확인란을 선택 하거나 실패 한 정책이 포함 된 행을 클릭 하면 평가에 실패 한 대상 인스턴스 옆의 **대상 세부 정보** 창에 확인란이 나타납니다. 확인란 중 하나를 선택 하면 **적용** 단추를 사용할 수 있게 됩니다. **적용**을 클릭 하면 선택한 대상 인스턴스에서 비규격 설정이 자동으로 업데이트 됩니다.  
  
    > [!CAUTION]  
    >  대상 인스턴스를 자동으로 업데이트하기 전에 정책 설정을 충분히 이해하고 있어야 합니다. 하나 이상의 확인란을 선택한 후에는 **스크립트**를 클릭 하 고 출력 위치를 선택 하 여 [!INCLUDE[tsql](../includes/tsql-md.md)] 변경 내용을 적용 하기 전에 기본 코드를 검토할 수 있도록 하는 것이 좋습니다.  
  
8.  정책에 대 한 자세한 결과를 보려면 **결과** 테이블에서 정책을 클릭 합니다. **대상 세부 정보** 테이블에는 각 인스턴스에 대 한 세부 정보가 표시 됩니다.  
  
## <a name="next-lesson"></a>다음 단원  
 [2단원: 일정에 따라 최선의 구현 방법 정책 평가](../../2014/tutorials/lesson-2-evaluate-best-practices-policies-on-a-scheduled-basis.md)  
  
## <a name="see-also"></a>참고 항목  
 [정책 기반 관리를 사용 하 여 모범 사례 모니터링 및 적용](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)   
 [중앙 관리 서버를 사용하여 여러 서버 관리](../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
