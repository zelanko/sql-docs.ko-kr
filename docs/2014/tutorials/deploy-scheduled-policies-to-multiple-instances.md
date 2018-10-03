---
title: 예약 된 정책을 여러 인스턴스에 배포 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: f551b8e8-3668-4ed4-852f-bae826254f4f
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: e0e98af473babc84863c8e0a1610107843ca76d5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48128273"
---
# <a name="deploy-scheduled-policies-to-multiple-instances"></a>여러 인스턴스에 예약된 정책 배포
  등록된 서버를 사용하면 중앙 위치에서 관리되는 서버로 예약된 정책을 배포할 수 있습니다. 로컬 서버 그룹 또는 중앙 관리 서버에서 예약된 정책을 배포할 수 있습니다.  
  
 이 태스크에서는 다음을 수행합니다.  
  
1.  이전 태스크에서 예약한 정책을 폴더로 내보냅니다.  
  
2.  예약된 정책을 등록된 서버로 관리되는 대상 인스턴스에 배포합니다.  
  
 이 단원에서는 이전 태스크를 완료한 컴퓨터에서 이러한 태스크를 수행합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 태스크의 선행 조건은 다음과 같습니다.  
  
-   이 단원에서 이전 태스크를 완료했어야 합니다.  
  
-   예약된 정책을 배포할 인스턴스에서 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 이상 버전을 실행하고 있어야 합니다. Automation을 수행하려면 정책을 로컬로 저장해야 합니다. 이 기능은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 이전의 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 버전에서는 지원되지 않습니다.  
  
-   예약된 된 정책을 배포 하려는 서버에서 등록 된 서버에 등록 되어야 합니다는 **로컬 서버 그룹** 또는 **중앙 관리 서버** 노드. 자세한 내용은 다음 항목을 참조하십시오.  
  
    -   [서버 그룹 만들기 또는 편집&#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
    -   [연결된 된 서버 등록 &#40;SQL Server Management Studio&#41;](../ssms/register-servers/register-a-connected-server-sql-server-management-studio.md)합니다.  
  
    -   [중앙 관리 서버 및 서버 그룹 만들기&#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)  
  
### <a name="to-export-the-scheduled-policies-as-xml-files"></a>예약된 정책을 .xml 파일로 내보내려면  
  
1.  이전 작업에서 예약 된 정책의 구성한 서버에서 확장 **관리**를 확장 하 고 **정책 관리**를 클릭 하 고 **정책**.  
  
2.  **보기** 메뉴에서 **개체 탐색기 정보**를 클릭합니다.  
  
3.  에 **개체 탐색기 정보** 창, 모두 예약 된 최선의 구현 방법 등록 된 서버를 통해 다른 서버에 배포 하려는 정책을 선택 합니다.  
  
    > [!NOTE]  
    >  클릭할 수는 **범주** 정책을 범주별으로 정렬 하려면 머리글입니다.  
  
4.  선택 영역을 마우스 오른쪽 단추로 누른 **정책 내보내기**합니다.  
  
5.  내보낼 여러 정책을 선택 하는 경우는 **폴더 찾아보기** 대화 상자에서 대상 폴더를 선택 하거나 새 폴더를 만듭니다. 이 단원에 대 한 경로 사용 하 여 새 폴더를 만듭니다 **C:\Scheduled_BP_Policies**를 클릭 하 고 **확인**합니다.  
  
     내보낼 정책을 하나만 선택 합니다 **정책 내보내기** 대화 상자에 경로 사용 하 여 새 폴더를 만듭니다 **C:\Scheduled_BP_Policies**, 클릭 **열기**를 클릭 하 고 **저장할**합니다.  
  
     .xml 정책 파일은 폴더 위치에 생성됩니다.  
  
### <a name="to-deploy-the-scheduled-policies-to-servers-that-are-managed-through-registered-servers"></a>예약된 정책을 등록된 서버를 통해 관리되는 서버에 배포하려면  
  
1.  **보기** 메뉴에서 **등록된 서버**를 클릭합니다.  
  
2.  확장 **데이터베이스 엔진**, 확장 **로컬 서버 그룹** 또는 **중앙 관리 서버**에 정책을 배포 하려는 노드를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **정책 가져오기**합니다.  
  
    > [!NOTE]  
    >  마우스 오른쪽 단추로 **로컬 서버 그룹** 또는 중앙 관리 서버 자체의 정책이 모든 관리 서버에 배포 됩니다. 특정 서버 그룹을 마우스 오른쪽 단추로 클릭하면 해당 그룹의 서버에만 정책이 배포됩니다. 등록된 특정 서버를 마우스 오른쪽 단추로 클릭하면 해당 서버에만 정책이 배포됩니다.  
  
3.  옆에 **가져올 파일**, 줄임표 단추 (**...** ).  
  
4.  에 **정책 선택** 대화 상자에서 예약된 된 정책을 저장 한 폴더 위치를 찾습니다. 예를 들어 위치를 찾습니다 **C:\Scheduled_BP_Policies**합니다.  
  
5.  대상 인스턴스를 가져오고 클릭 하려는 정책을 선택 **열려**합니다.  
  
6.  에 **가져오기** 대화 상자의 합니다 **정책 상태** 목록에서 원하는 정책 상태를 선택 합니다. 가져올 때 정책 상태를 유지하거나 정책을 설정 또는 해제하도록 선택할 수 있습니다. 정책은 예약 실행하도록 설정해야 합니다.  
  
7.  클릭 **확인** 정책을 모든 대상 인스턴스로 가져올 합니다.  
  
    > [!NOTE]  
    >  오류가 발생 하는 경우는 **가져오기** 대화 상자가 사라지지 않습니다. 클릭 합니다 **로그** 메시지를 검토 하는 페이지입니다. 클릭 **취소** 대화 상자를 닫습니다.  
  
8.  대상 인스턴스의 정책을 보려면, 인스턴스에 연결 하 고 개체 탐색기를 열고 확장 **관리**를 차례로 확장 하 고 **정책을**합니다. 가져온된 정책이 표시 되어야 합니다 **정책을** 노드. 각 정책을 두 번 클릭하면 일정을 보거나 설정을 변경할 수 있습니다.  
  
    > [!NOTE]  
    >  예약된 정책 실행 이후 평가 결과를 보려면 대상 인스턴스에 대한 정책 기록 로그를 엽니다. 로그를 열려면 마우스 오른쪽 단추로 클릭 **정책 관리**를 클릭 하 고 **기록 보기**합니다.  
  
## <a name="summary"></a>요약  
 이 자습서에서는 하나 이상의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 대해 최선의 구현 방법 정책에 대한 요청 시 평가와 예약된 평가를 모두 수행하는 방법을 살펴보았습니다.  
  
## <a name="next"></a>다음  
 이 자습서를 마칩니다. 참조 시작으로 돌아가려면 [자습서: 정책 기반 관리에서 모범 사례를 평가](../../2014/tutorials/tutorial-evaluating-best-practices-by-using-policy-based-management.md)합니다.  
  
 목록을 보려면 [!INCLUDE[ssDE](../includes/ssde-md.md)] 자습서, 클릭 [데이터베이스 엔진 자습서](../relational-databases/database-engine-tutorials.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [정책 기반 관리를 사용하여 서버 관리](../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
