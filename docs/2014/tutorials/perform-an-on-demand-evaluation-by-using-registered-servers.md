---
title: 등록 된 서버를 사용 하 여 요청 시 평가 수행 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security"
ms.topic: conceptual
ms.assetid: c14034ef-6e0b-4df5-8072-bfb8d90b3172
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 31282041abe538bd51ba4b1367f70cd3c5fa3d5b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56030794"
---
# <a name="perform-an-on-demand-evaluation-by-using-registered-servers"></a>등록된 서버를 사용하여 요청 시 평가 수행
  등록된 서버를 사용하여 하나 이상의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 대해 최선의 구현 방법 정책의 요청 시 평가를 수행할 수 있습니다. 로컬 서버 그룹 또는 중앙 관리 서버를 사용할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 또는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 이상 버전이 실행되는 서버 그룹 멤버에 대해 최선의 구현 방법 정책의 요청 시 평가를 수행할 수 있습니다. 그러나 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 또는 [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]에서 지원되지 않는 정책에서 참조하는 속성이 있는 경우 예외 오류가 발생할 수 있습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 등록된 서버에서 하나 이상의 서버 등록을 구성한 경우에만 이 태스크를 수행할 수 있습니다. 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [서버 그룹 만들기 또는 편집&#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
-   [연결된 된 서버 등록 &#40;SQL Server Management Studio&#41;](../ssms/register-servers/register-a-connected-server-sql-server-management-studio.md)합니다.  
  
-   [중앙 관리 서버 및 서버 그룹 만들기&#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)  
  
### <a name="to-evaluate-best-practices-policies-against-a-server-group"></a>서버 그룹에 대해 최선의 구현 방법 정책을 평가하려면  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 **보기** 메뉴에서 **등록된 서버**를 클릭합니다.  
  
2.  확장 **데이터베이스 엔진**, 다음 중 하나를 확장 하 고 **로컬 서버 그룹**, 또는 **중앙 관리 서버**구성에 따라 합니다.  
  
3.  다음 중 하나를 수행합니다.  
  
    -   로컬 서버 그룹에 의해 관리 되는 모든 서버 또는 중앙 관리 서버에 대해 정책을 평가 하려면 로컬 서버 그룹 이름 또는 중앙 관리 서버 이름을 마우스 오른쪽 단추로 클릭 한 다음 클릭 **정책 평가** .  
  
        > [!NOTE]  
        >  중앙 관리 서버를 통해 정책을 평가하면 중앙 관리 서버 자체에 대해서는 정책이 평가되지 않습니다.  
  
    -   특정 서버 또는 서버 그룹에 대해 정책을 평가 하려면 확장 **로컬 서버 그룹** 또는 중앙 관리 서버 이름, 서버 또는 서버 그룹에 대해 정책을 평가 하 고 클릭 하려는 마우스 오른쪽 단추로 클릭 **정책을 평가**합니다.  
  
4.  에 **정책 평가** 대화 상자에서 다음을 **원본** 상자에서 줄임표 (**...** ) 단추입니다.  
  
5.  에 **원본 선택** 대화 상자에서 선택할 수 있습니다 **파일** 또는 **Server** 를 평가할 정책 파일의 원본으로 합니다. 클릭 하면 **Server**, 로컬 또는 원격 서버에서 정책 기반 관리에 이전에 가져온 모든 최선의 구현 방법 정책의 요청 시 평가 수행할 수 있습니다. 이 자습서에서는 클릭 **파일**, 한 다음 평가할 개별 정책 파일을 선택 합니다. 이렇게 하려면 다음 단계를 수행합니다.  
  
    1.  클릭 **파일**합니다.  
  
    2.  옆에 **파일**, 줄임표 (**...** ) 단추입니다.  
  
    3.  평가 하 고 클릭 한 다음에 하나 이상의.xml 정책 파일 선택 **열려**합니다.  
  
         선택한 파일의 목록에 표시 합니다 **파일** 상자입니다.  
  
    4.  에 **원본 선택** 대화 상자, 클릭 **확인**합니다.  
  
    5.  경우는 **정책을 로드** 대화 상자가 나타나면 **닫기**합니다.  
  
     선택한 정책에 나열 됩니다는 **정책 선택** 페이지입니다. 정책 옆의 경고 아이콘은 정책에 스크립트가 포함되어 있다는 것을 나타냅니다.  
  
6.  클릭 **평가** 정책을 평가 하려면.  
  
7.  일부 정책 실패의 경우 정책 기반 관리를 사용하면 대상에서 정책 준수를 즉시 강제할 수 있습니다. 이러한 실패의 경우 실패한 정책 옆에 확인란이 나타납니다. 확인란에서 확인란을 선택 하거나 실패 한 정책 사용 하 여 행을 클릭 하는 경우에 표시 된 **대상 세부 정보** 평가 하지 못한 대상 인스턴스 옆에 있는 창입니다. 확인란을 선택 합니다 **적용** 단추를 사용할 수 있습니다. 클릭 하면 **적용**, 선택한 대상 인스턴스에서 비호환 설정이 자동으로 업데이트 됩니다.  
  
    > [!CAUTION]  
    >  대상 인스턴스를 자동으로 업데이트하기 전에 정책 설정을 충분히 이해하고 있어야 합니다. 하나 이상의 확인란을 선택한 후 클릭 하는 것이 좋습니다 **스크립트**, 기본 검토할 수 있도록 출력 위치를 선택 하 고 [!INCLUDE[tsql](../includes/tsql-md.md)] 코드 변경 내용을 적용 하기 전에 합니다.  
  
8.  정책에 대 한 자세한 결과 보려면에서 정책을 클릭 합니다 **결과** 테이블입니다. 합니다 **대상 세부 정보** 테이블 각 인스턴스에 대 한 세부 정보를 표시 합니다.  
  
## <a name="next-lesson"></a>다음 단원  
 [2단원: 일정에 따라 최선의 구현 방법 정책 평가](../../2014/tutorials/lesson-2-evaluate-best-practices-policies-on-a-scheduled-basis.md)  
  
## <a name="see-also"></a>관련 항목  
 [모니터링 및 정책 기반 관리를 사용 하 여 모범 사례 적용](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)   
 [중앙 관리 서버를 사용하여 여러 서버 관리](../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
