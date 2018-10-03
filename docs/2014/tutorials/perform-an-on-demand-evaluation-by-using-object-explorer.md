---
title: 개체 탐색기를 사용 하 여 요청 시 평가 수행 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: ee6d3b79-18bc-49d3-8a1d-0c0905b990f0
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: f950b99b7de4b7e81d75ed9decee47f74a785206
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48098113"
---
# <a name="perform-an-on-demand-evaluation-by-using-object-explorer"></a>개체 탐색기를 사용하여 요청 시 평가 수행
  이 태스크에서는 개체 탐색기를 사용하여 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]의 단일 인스턴스에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 최선의 구현 방법 정책에 대한 요청 시 평가를 수행합니다.  
  
> [!NOTE]  
>  등록된 서버를 통해 단일 인스턴스에서 정책을 평가할 수도 있습니다. 자세한 내용은 [by Using Registered Servers 주문형 평가 수행할](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 단원은 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 버전을 사용합니다.  
  
> [!NOTE]  
>  실행 중인 인스턴스에 대해 최선의 구현 방법 정책의 요청 시 평가 수행 하려면 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], 항목의 절차를 사용 해야 [는 On-demand Evaluation by Using Registered Servers 수행](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)합니다.  
  
### <a name="to-perform-an-on-demand-evaluation-by-using-object-explorer"></a>개체 탐색기를 사용하여 요청 시 평가를 수행하려면  
  
1.  [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]를 시작하고 [!INCLUDE[ssDE](../includes/ssde-md.md)]에 연결합니다.  
  
2.  개체 탐색기에서 확장 **관리**, 확장 **정책 관리**를 마우스 오른쪽 단추로 클릭 **정책**를 클릭 하 고 **평가**합니다.  
  
    > [!NOTE]  
    >  기본적으로 로컬 인스턴스가 정책의 원본으로 사용됩니다. 이전에 최선의 구현 방법 정책을 가져온 경우 만들어진 다른 정책과 함께 해당 정책이 나열됩니다. 가져온된 최선의 구현 방법 정책 중 하나를 선택 하 고 클릭 **평가**합니다. 최선의 구현 방법 정책을 가져오지 않은 경우 이 절차를 계속합니다.  
  
3.  에 **정책 평가** 대화 상자에서 다음을 **원본** 상자에서 줄임표 (**...** ) 단추입니다.  
  
4.  에 **원본 선택** 대화 상자에서 선택할 수 있습니다 **파일** 또는 **Server** 를 평가할 정책 파일의 원본으로 합니다. 클릭 하면 **Server**, 로컬 또는 원격 서버에서 정책 기반 관리에 이전에 가져온 모든 최선의 구현 방법 정책의 요청 시 평가 수행할 수 있습니다. 이 자습서에서는 클릭 **파일**, 한 다음 평가할 개별 정책 파일을 선택 합니다. 이렇게 하려면 다음 단계를 수행합니다.  
  
    1.  클릭 **파일**합니다.  
  
    2.  옆에 **파일**, 줄임표 (**...** ) 단추입니다.  
  
    3.  에 **정책 선택** 대화 상자에서 최선의 구현 방법 정책을 포함 하는 다음 폴더를 찾습니다.  
  
         **C:\Program 파일 (x86) \Microsoft SQL Server\110\Tools\Policies\DatabaseEngine\1033**  
  
        > [!NOTE]  
        >  파일 경로는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 프로그램 파일의 설치 위치, 32비트 운영 체제를 실행하는지 아니면 64비트 운영 체제를 실행하는지 여부 및 언어 식별자에 따라 달라질 수 있습니다.  
  
    4.  평가 하 고 클릭 한 다음에 하나 이상의.xml 정책 파일 선택 **열려**합니다.  
  
         선택한 파일의 목록에 표시 합니다 **파일** 상자입니다.  
  
    5.  에 **원본 선택** 대화 상자, 클릭 **확인**합니다.  
  
    6.  경우는 **정책을 로드** 대화 상자가 나타나면 **닫기**합니다.  
  
     선택한 정책에 나열 됩니다는 **정책 선택** 페이지입니다. 정책 옆의 경고 아이콘은 정책에 스크립트가 포함되어 있다는 것을 나타냅니다.  
  
5.  클릭 **평가** 정책을 평가 하려면.  
  
     에 **결과** 테이블 결과 각 정책에 나열 됩니다. 빨간색 "x" 아이콘은 정책 준수에 실패했음을 나타냅니다.  
  
6.  일부 정책 실패의 경우 정책 기반 관리를 사용하면 대상에서 정책 준수를 즉시 강제할 수 있습니다. 이러한 실패의 경우 실패한 정책 옆에 확인란이 나타납니다. 확인란을 선택 하는 경우는 **적용** 단추를 사용할 수 있습니다. 클릭 하면 **적용**, 대상 인스턴스에서 비호환 설정이 자동 업데이트 됩니다.  
  
    > [!CAUTION]  
    >  대상 인스턴스를 자동으로 업데이트하기 전에 정책 설정을 충분히 이해하고 있어야 합니다. 하나 이상의 확인란을 선택한 후 클릭 하는 것이 좋습니다 **스크립트**, 기본 검토할 수 있도록 출력 위치를 선택 하 고 [!INCLUDE[tsql](../includes/tsql-md.md)] 코드 변경 내용을 적용 하기 전에 합니다.  
  
7.  정책에 대 한 자세한 결과 보려면에서 정책을 클릭 합니다 **결과** 테이블입니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [등록된 서버를 사용하여 요청 시 평가 수행](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)  
  
  
