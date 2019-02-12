---
title: 데이터 원본 (기본 데이터 마이닝 자습서) 만들기 | Microsoft Docs
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
ms.openlocfilehash: eb18bc37f63b74981fcccbcb889bd80dcb816d12
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56042624"
---
# <a name="creating-a-data-source-basic-data-mining-tutorial"></a>데이터 원본 만들기(기본 데이터 마이닝 자습서)
  A *데이터 원본* 데이터 연결이 저장 하 고 프로젝트에서 관리 하 고 배포에 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스입니다. 데이터 원본에는 원본 데이터가 있는 서버 및 데이터베이스의 이름뿐만 아니라 필요한 기타 연결 속성이 포함됩니다.  
  
> [!IMPORTANT]  
>  데이터베이스의 이름은 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]입니다. 이 데이터베이스를 아직 설치 하지 않은 경우 참조를 [Microsoft SQL Sample Databases](https://go.microsoft.com/fwlink/?LinkId=88417) 페이지입니다.  
  
### <a name="to-create-a-data-source"></a>데이터 원본을 만들려면  
  
1.  **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **데이터 원본** 폴더를 선택 **새 데이터 원본을**합니다.  
  
2.  에 **데이터 원본 마법사 시작** 페이지에서 클릭 **다음**합니다.  
  
3.  에 **연결 정의 방법 선택** 페이지에서 클릭 **새로 만들기** 에 대 한 연결을 추가 하는 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 데이터베이스.  
  
4.  에 **공급자** 목록의 **연결 관리자**를 선택 **네이티브 OLE DB\SQL Server Native Client 11.0**합니다.  
  
5.  에 **서버 이름** 상자, 입력 또는 설치 된 서버의 이름을 선택 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]합니다.  
  
     예를 들어 입력 **localhost** 데이터베이스가 로컬 서버에서 호스팅되는 경우.  
  
6.  에 **서버에 로그온** 그룹에서 **Windows 인증을 사용 하 여**입니다.  
  
    > [!IMPORTANT]  
    >  가능하면 구현자가 SQL Server 인증보다 더 안전한 인증 방법을 제공하는 Windows 인증을 사용해야 합니다. 그러나 SQL Server 인증은 이전 버전과의 호환성을 위해 제공됩니다. 인증 방법에 대 한 자세한 내용은 참조 하세요. [데이터베이스 엔진 구성-계정 프로 비전](../../2014/sql-server/install/database-engine-configuration-account-provisioning.md)합니다.  
  
7.  에 **데이터베이스 이름 선택 또는 입력** 목록에서 선택 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 을 클릭 한 다음 **확인**합니다.  
  
8.  **다음**을 클릭합니다.  
  
9. 에 **가장 정보** 페이지에서 클릭 **서비스 계정을 사용**를 클릭 하 고 **다음**합니다.  
  
     에 **마법사 완료** 페이지에서, 기본적으로 데이터 원본을 지정 하는 Adventure Works DW 2012 알 수 있습니다.  
  
10. **마침**을 클릭합니다.  
  
     새 데이터 원본인 Adventure Works DW 2012 나타나는 합니다 **데이터 원본** 솔루션 탐색기에서 폴더입니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [만들기는 데이터 원본 뷰 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/creating-a-data-source-view-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>단원의 이전 태스크  
 [만들기는 Analysis Services 프로젝트 &#40;기본 데이터 마이닝 자습서&#41;](../../2014/tutorials/creating-an-analysis-services-project-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [데이터 원본 만들기&#40;SSAS 다차원&#41;](../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)   
 [데이터 원본 정의](../analysis-services/lesson-1-2-defining-a-data-source.md)   
 [가장 옵션 설정 & #40; SSAS-다차원 데이터 & #41;](../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md)  
  
  
