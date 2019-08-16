---
title: 데이터 원본 만들기 (기본 데이터 마이닝 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d7107c32-69ed-49a8-9b6e-32753eebf42c
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3f85320a99c901a2fd71c9048750825569559099
ms.sourcegitcommit: f5807ced6df55dfa78ccf402217551a7a3b44764
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69494021"
---
# <a name="creating-a-data-source-basic-data-mining-tutorial"></a>데이터 원본 만들기(기본 데이터 마이닝 자습서)
  *데이터 원본은* 프로젝트에서 저장 및 관리 되 고 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 배포 되는 데이터 연결입니다. 데이터 원본에는 원본 데이터가 있는 서버 및 데이터베이스의 이름뿐만 아니라 필요한 기타 연결 속성이 포함됩니다.  
  
> [!IMPORTANT]  
>  데이터베이스의 이름은 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]입니다. 이 데이터베이스를 아직 설치 하지 않은 경우 [MICROSOFT SQL 예제 데이터베이스](https://go.microsoft.com/fwlink/?LinkId=88417) 페이지를 참조 하세요.  
  
### <a name="to-create-a-data-source"></a>데이터 원본을 만들려면  
  
1.  **솔루션 탐색기**에서 **데이터 원본** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **새 데이터 원본**을 선택 합니다.  
  
2.  **데이터 원본 마법사 시작** 페이지에서 **다음**을 클릭 합니다.  
  
3.  **연결 정의 방법 선택** 페이지에서 **새로 만들기** 를 클릭 하 여 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 데이터베이스에 대 한 연결을 추가 합니다.  
  
4.  **연결 관리자**의 **공급자** 목록에서 **네이티브 OLE Db\sql Server native Client 11.0**를 선택 합니다.  
  
5.  **서버 이름** 상자에를 설치한 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]서버의 이름을 입력 하거나 선택 합니다.  
  
     예를 들어 데이터베이스가 로컬 서버에서 호스트 되는 경우 **localhost** 를 입력 합니다.  
  
6.  서버에 **로그온** 그룹에서 **Windows 인증 사용**을 선택 합니다.  
  
    > [!IMPORTANT]  
    >  가능하면 구현자가 SQL Server 인증보다 더 안전한 인증 방법을 제공하는 Windows 인증을 사용해야 합니다. 그러나 SQL Server 인증은 이전 버전과의 호환성을 위해 제공됩니다. 인증 방법에 대 한 자세한 내용은 [데이터베이스 엔진 구성-계정 프로 비전](../../2014/sql-server/install/database-engine-configuration-account-provisioning.md)을 참조 하세요.  
  
7.  **데이터베이스 이름 선택 또는 입력** 목록에서를 선택 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 하 고 **확인**을 클릭 합니다.  
  
8.  **다음**을 클릭합니다.  
  
9. **가장 정보** 페이지에서 **서비스 계정 사용**을 클릭 하 고 **다음**을 클릭 합니다.  
  
     **마법사 완료** 페이지에서는 기본적으로 데이터 원본의 이름이 놀이 Works DW 2012입니다.  
  
10. **마침**을 클릭합니다.  
  
     새 데이터 원본인 어드벤처 DW 2012는 솔루션 탐색기의 **데이터 원본** 폴더에 표시 됩니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [데이터 원본 뷰 &#40;만들기 기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/creating-a-data-source-view-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>단원의 이전 태스크  
 [Analysis Services 프로젝트 &#40;기본 데이터 마이닝 자습서 만들기&#41;](../../2014/tutorials/creating-an-analysis-services-project-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [데이터 원본 만들기&#40;SSAS 다차원&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional)   
 [데이터 원본 정의](../analysis-services/lesson-1-2-defining-a-data-source.md)   
 [가장 옵션 설정 & #40; SSAS-다차원 데이터 & #41;](https://docs.microsoft.com/analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional)  
  
  
