---
title: Analysis Services 인스턴스 이름 바꾸기 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- instances of Analysis Services, renaming
- renaming instances of Analysis Services
- names [Analysis Services], renaming instances
- names [Analysis Services]
ms.assetid: 87494741-4a2e-4fed-8061-418fd1e111c3
caps.latest.revision: 49
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0dfa3a42caf787fad5e8eb64e5bdbab38997640b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37326813"
---
# <a name="rename-an-analysis-services-instance"></a>Analysis Services 인스턴스 이름 바꾸기
  기존 인스턴스의 이름을 바꿀 수 있습니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 사용 하 여 합니다 **인스턴스 이름 바꾸기** 대화 상자.  
  
> [!IMPORTANT]  
>  인스턴스의 이름을 바꾸는 동안 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 이름 바꾸기 도구는 승격된 권한으로 실행되어 해당 인스턴스와 연결된 레지스트리 항목, Windows 서비스 이름 및 보안 계정을 업데이트합니다. 이러한 동작이 수행되도록 하려면 이 도구를 로컬 시스템 관리자로 실행하십시오.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 이름 바꾸기 도구는 원래 인스턴스에 대해 생성된 프로그램 폴더를 수정하지 않습니다. 이름을 바꾸는 인스턴스와 일치하도록 프로그램 폴더 이름을 수정하지 마십시오. 프로그램 폴더 이름을 변경하면 설치 프로그램이 설치를 복구하거나 제거할 수 없습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 이름 바꾸기 도구는 클러스터 환경에서 사용할 수 없습니다.  
  
### <a name="to-rename-an-instance-of-analysis-services"></a>Analysis Services의 인스턴스 이름을 변경하려면  
  
1.  시작 합니다 **인스턴스 이름 바꾸기** 도구인 **asinstancerename.exe**, C:\Program Files\Microsoft SQL Server\110\Tools\Binn\ManagementStudio에서.  
  
2.  **인스턴스 이름 바꾸기** 대화 상자의 **이름을 바꿀 인스턴스** 목록에서 이름을 바꿀 인스턴스를 선택합니다.  
  
3.  **새 인스턴스 이름** 입력란에 인스턴스의 새 이름을 입력합니다.  
  
4.  사용자 이름과 암호가 올바른지 확인하고 **이름 바꾸기**를 클릭합니다.  
  
     이름을 변경하는 동안 Analysis Services 인스턴스가 중지되고 다시 시작됩니다.  
  
### <a name="post-rename-checklist"></a>이름을 바꾼 후 검사할 목록  
  
1.  이름을 바꾼 인스턴스에서 실행되는 데이터베이스에 대한 액세스를 다시 시작하려면 Excel 또는 다른 클라이언트 응용 프로그램에서 데이터 연결을 수동으로 업데이트해야 합니다. 이름을 바꾼 인스턴스를 참조할 수 있는 Reporting Services 공유 데이터 원본, Excel ODC 파일 또는 BI 의미 체계 모델 연결 파일 등 미리 정의된 연결도 확인합니다. 자세한 내용은 [Analysis Services에 연결](connect-to-analysis-services.md)을 참조하세요.  
  
2.  데이터베이스를 백업, 동기화 또는 처리하는 데 일상적으로 사용하는 PowerShell 스크립트 또는 AMO 스크립트를 업데이트합니다.  
  
3.  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 사용하는 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]프로젝트의 프로젝트 속성을 업데이트합니다. 테이블 형식 모드 서버 인스턴스의 경우 model.bim 파일의 작업 영역 서버 속성과 프로젝트의 서버 속성을 업데이트해야 합니다.  
  
4.  서비스 계정을 지정한 방법에 따라 서비스에 데이터 액세스 권한을 부여하는 데이터베이스 로그인 또는 파일 사용 권한을 업데이트해야 할 수도 있습니다. 예를 들어 서비스 계정을 사용하여 데이터를 처리하거나 다른 서버의 연결된 개체에 액세스 하는 경우가 여기에 해당합니다.  
  
     가상 계정을 사용하여 서비스를 프로비전하는 경우 데이터베이스 로그인 또는 파일 사용 권한을 업데이트해야 합니다. 가상 계정은 인스턴스 이름을 사용하여 생성되므로 인스턴스의 이름을 바꾸는 경우 가상 계정도 동시에 업데이트됩니다. 즉 이전 인스턴스에 대해 만든 이전 로그인 또는 사용 권한은 더 이상 유효하지 않습니다.  
  
     다음 예에서는 이러한 내용을 보여 줍니다. 기본 가상 계정을 사용하여 “Tabular”라는 인스턴스로 테이블 형식 모드 서버를 설치한 경우 다음과 같은 구성이 생성됩니다.  
  
    1.  Instance name = \<server>\TABULAR  
  
    2.  Service name = MSOLAP$TABULAR  
  
    3.  Virtual account = NT Service\ MSOLAP$TABULAR  
  
     이제 "TAB2"로 인스턴스 이름을 바꾼다고 가정합니다. 이름을 변경하면 구성이 다음과 같이 변경됩니다.  
  
    1.  Instance name = \<server>\TAB2  
  
    2.  Service name = MSOLAP$TAB2  
  
    3.  Virtual account = NT Service\ MSOLAP$TAB2  
  
     이전에 “NT Service\ MSOLAP$TABULAR”에 부여된 데이터베이스 및 파일 사용 권한은 더 이상 유효하지 않음을 알 수 있습니다. 서비스가 수행하는 태스크 및 작업이 이전과 같이 실행되도록 하려면 “NT Service\ MSOLAP$TAB2”에 새 데이터베이스 및 파일 사용 권한을 부여해야 합니다.  
  
  
