---
title: 개체 탐색기 |를 사용 하 여 요청 시 평가 수행 Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: ee6d3b79-18bc-49d3-8a1d-0c0905b990f0
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 8d2aadd055334c7ee64871c2fdfe5239c9849e90
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68210942"
---
# <a name="perform-an-on-demand-evaluation-by-using-object-explorer"></a>개체 탐색기를 사용하여 요청 시 평가 수행
  이 태스크에서는 개체 탐색기를 사용하여 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]의 단일 인스턴스에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 최선의 구현 방법 정책에 대한 요청 시 평가를 수행합니다.  
  
> [!NOTE]  
>  등록된 서버를 통해 단일 인스턴스에서 정책을 평가할 수도 있습니다. 자세한 내용은 [등록 된 서버를 사용 하 여 요청 시 평가 수행](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)을 참조 하세요.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 단원은 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 버전을 사용합니다.  
  
> [!NOTE]  
>  실행 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]중인 인스턴스에 대해 최선의 구현 방법 정책의 요청 시 평가를 수행 하려면 [등록 된 서버를 사용 하 여 요청 시 평가 수행](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)항목의 절차를 사용 해야 합니다.  
  
### <a name="to-perform-an-on-demand-evaluation-by-using-object-explorer"></a>개체 탐색기를 사용하여 요청 시 평가를 수행하려면  
  
1.  [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]를 시작하고 [!INCLUDE[ssDE](../includes/ssde-md.md)]에 연결합니다.  
  
2.  개체 탐색기에서 **관리**, **정책 관리**를 차례로 확장 하 고 **정책**을 마우스 오른쪽 단추로 클릭 한 다음 **평가**를 클릭 합니다.  
  
    > [!NOTE]  
    >  기본적으로 로컬 인스턴스가 정책의 원본으로 사용됩니다. 이전에 최선의 구현 방법 정책을 가져온 경우 만들어진 다른 정책과 함께 해당 정책이 나열됩니다. 가져온 모범 사례 정책 중 하나를 선택 하 고 **평가**를 클릭할 수 있습니다. 최선의 구현 방법 정책을 가져오지 않은 경우 이 절차를 계속합니다.  
  
3.  **정책 평가** 대화 상자에서 **원본** 상자 옆의 줄임표 (**...**) 단추를 클릭 합니다.  
  
4.  **원본 선택** 대화 상자에서 평가할 정책 파일의 원본으로 **파일** 또는 **서버** 를 선택할 수 있습니다. **서버**를 클릭 하면 로컬 또는 원격 서버에서 정책 기반 관리로 이전에 가져온 모범 사례 정책에 대 한 요청 시 평가를 수행할 수 있습니다. 이 자습서에서는 **파일**을 클릭 한 다음 평가할 개별 정책 파일을 선택 합니다. 이렇게 하려면 다음 단계를 따르십시오.  
  
    1.  **파일**을 클릭 합니다.  
  
    2.  **파일**옆에 있는 줄임표 (**...**) 단추를 클릭 합니다.  
  
    3.  **정책 선택** 대화 상자에서 최선의 구현 방법 정책이 포함 된 다음 폴더를 찾습니다.  
  
         **C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Policies\DatabaseEngine\1033**  
  
        > [!NOTE]  
        >  파일 경로는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 프로그램 파일의 설치 위치, 32비트 운영 체제를 실행하는지 아니면 64비트 운영 체제를 실행하는지 여부 및 언어 식별자에 따라 달라질 수 있습니다.  
  
    4.  평가할 하나 이상의 .xml 정책 파일을 선택 하 고 **열기**를 클릭 합니다.  
  
         선택한 파일의 목록이 **파일** 상자에 나타납니다.  
  
    5.  **원본 선택** 대화 상자에서 **확인**을 클릭 합니다.  
  
    6.  **정책 로드 중** 대화 상자가 나타나면 **닫기**를 클릭 합니다.  
  
     선택한 정책이 **정책 선택** 페이지에 나열 됩니다. 정책 옆의 경고 아이콘은 정책에 스크립트가 포함되어 있다는 것을 나타냅니다.  
  
5.  **평가** 를 클릭 하 여 정책을 평가 합니다.  
  
     **결과** 테이블에 각 정책에 대 한 결과가 나열 됩니다. 빨간색 "x" 아이콘은 정책 준수에 실패했음을 나타냅니다.  
  
6.  일부 정책 실패의 경우 정책 기반 관리를 사용하면 대상에서 정책 준수를 즉시 강제할 수 있습니다. 이러한 실패의 경우 실패한 정책 옆에 확인란이 나타납니다. 이 확인란을 선택 하면 **적용** 단추를 사용할 수 있게 됩니다. **적용**을 클릭 하면 대상 인스턴스에서 비규격 설정이 자동으로 업데이트 됩니다.  
  
    > [!CAUTION]  
    >  대상 인스턴스를 자동으로 업데이트하기 전에 정책 설정을 충분히 이해하고 있어야 합니다. 하나 이상의 확인란을 선택한 후에는 **스크립트**를 클릭 하 고 출력 위치를 선택 하 여 변경 내용을 적용 하기 전에 기본 [!INCLUDE[tsql](../includes/tsql-md.md)] 코드를 검토할 수 있도록 하는 것이 좋습니다.  
  
7.  정책에 대 한 자세한 결과를 보려면 **결과** 테이블에서 정책을 클릭 합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [등록된 서버를 사용하여 요청 시 평가 수행](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)  
  
  
