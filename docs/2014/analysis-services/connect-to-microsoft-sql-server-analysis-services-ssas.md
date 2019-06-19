---
title: Microsoft SQL Server Analysis Services (SSAS)에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connsqlserveras.f1
ms.assetid: 7f3244ee-b690-471c-893d-68e361c2d416
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fe8eee02d019b5cf68e257b3fac4266a18ead795
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66087031"
---
# <a name="connect-to-microsoft-sql-server-analysis-services-ssas"></a>Microsoft SQL Server Analysis Services에 연결(SSAS)
  이 페이지의 **테이블 가져오기 마법사** Microsoft SQL Server Analysis Services 큐브 또는 SharePoint에서 호스팅되는 PowerPivot 통합 문서에서 데이터를 가져오기 위한 설정을 지정할 수 있습니다. [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 마법사에 액세스하려면 **모델** 메뉴에서 **데이터 원본에서 가져오기**를 클릭합니다.  
  
 데이터 원본에 연결하려면 컴퓨터에 적절한 공급자를 설치해야 합니다.  
  
> [!NOTE]  
>  이 페이지에서 데이터베이스를 선택하는 경우 현재 사용자의 자격 증명이 사용됩니다. 하지만 가장 정보 페이지에 지정된 사용자에게 선택한 데이터베이스를 읽을 수 있는 권한이 없는 경우에는 가져오기 작업이 실패합니다.  
  
## <a name="uielement-list"></a>UIElement 목록  
 **연결 이름**  
 이 데이터 원본 연결의 고유 이름을 입력합니다. 이 이름은 반드시 입력해야 합니다.  
  
 **서버 또는 파일 이름**  
 다음 중 하나를 입력합니다.  
  
-   연결할 SQL Server Analysis Services 서버의 이름이나 IP 주소를 입력합니다.  
  
     마침표(.), (local) 또는 localhost를 사용하여 로컬 서버를 지정할 수 있습니다.  
  
-   SharePoint에 게시할 PowerPivot 통합 문서의 URL을 입력합니다.  
  
 **Windows 인증 사용**  
 Windows 인증을 사용하여 SQL Server Analysis Services 서버에 연결할지 여부를 지정합니다.  
  
 Windows 인증 모드에서는 사용자가 Windows 사용자 계정을 통해 연결할 수 있습니다. 가능하면 Windows 인증을 사용하십시오.  
  
 Windows 인증을 사용하는 경우 현재 사용자의 자격 증명을 사용하여 테이블 속성 창 및 가져오기 마법사에서 데이터를 미리 보거나 필터링합니다. 이러한 자격 증명은 데이터를 가져오거나 새로 고칠 때는 사용되지 않습니다. 이 경우에는 가장 정보 페이지에서 지정한 Windows 자격 증명이 사용됩니다.  
  
 **SQL Server 인증 사용**  
 SQL Server 인증을 사용하여 SQL Server Analysis Services 서버에 연결할지 여부를 지정합니다.  
  
 SQL Server 인증을 사용하는 경우 SQL Server는 SQL Server 로그인 계정이 설정되어 있고 지정한 암호가 이전에 기록한 암호와 일치하는지를 자체적으로 확인하여 인증을 수행합니다.  
  
 SQL Server 인증은 데이터 원본에 대한 연결 문자열을 구성할 때 사용됩니다. 이러한 자격 증명은 테이블 속성 창과 가져오기 마법사에서 데이터를 미리 보거나 필터링할 때도 사용됩니다. 이러한 자격 증명은 데이터를 가져오거나 새로 고칠 때는 사용되지 않습니다. 이 경우에는 가장 정보 페이지에서 지정한 Windows 자격 증명이 사용됩니다.  
  
 **사용자 이름**  
 데이터베이스 연결의 사용자 이름을 지정합니다. 이 옵션은 Windows 인증을 사용하여 연결하도록 선택한 경우에만 사용할 수 있습니다.  
  
 **암호**  
 데이터베이스 연결의 암호를 지정합니다. 이 옵션은 SQL Server 인증을 사용하여 연결하도록 선택한 경우에만 편집할 수 있습니다.  
  
 **암호 저장**  
 **암호** 상자에 입력한 암호를 저장할지 여부를 지정합니다. 이 옵션은 SQL Server 인증을 사용하여 연결하도록 선택한 경우에만 사용할 수 있습니다.  
  
 **데이터베이스 이름**  
 데이터베이스 목록에서 데이터베이스를 선택합니다.  
  
 **고급**  
 **고급 속성 설정** 대화 상자를 사용하여 추가 연결 속성을 설정합니다. 자세한 내용은 [고급 속성 설정&#40;SSAS&#41;](set-advanced-properties-ssas.md)을 참조하세요.  
  
 **연결 테스트**  
 현재 설정을 사용하여 데이터 원본에 대한 연결을 설정해 봅니다. 연결이 성공적인지 여부를 나타내는 메시지가 표시됩니다.  
  
  
