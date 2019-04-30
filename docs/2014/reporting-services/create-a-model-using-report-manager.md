---
title: 보고서 관리자를 사용 하 여 모델 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report models [Reporting Services], creating
- Report Manager [Reporting Services], model creation
ms.assetid: 8e5d2bd3-48ec-45f3-afee-6d86797c8f28
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 07865f96b0e4086af346ffc076b1df6d07cda6cd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63265965"
---
# <a name="create-a-model-using-report-manager"></a>보고서 관리자를 사용하여 모델 만들기
  보고서 관리자를 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 큐브, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스 또는 Oracle 데이터베이스에서 모델을 생성할 수 있습니다. 보고서 모델은 보고서 서버에 게시된 공유 데이터 원본에서 생성됩니다. 공유 데이터 원본이 없는 경우 새로 만들어야 합니다.  
  
 생성되는 보고서 모델은 전적으로 공유 데이터 원본의 스키마를 기반으로 합니다. 모델에 포함될 데이터 원본 부분을 선택하거나 생성되는 모델의 규칙 또는 메타데이터를 편집할 수는 없습니다. 그러나 모델이 생성된 후 속성을 설정하고 모델 전체 또는 일부에 대한 액세스를 제한하는 역할 할당을 정의할 수 있습니다.  
  
> [!NOTE]  
>  보고서 관리자를 사용 하 여 생성 된 Oracle 기반 모델을 또는 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2007 [!INCLUDE[SPS2010](../includes/sps2010-md.md)] Oracle 데이터 원본에 연결할 때 사용할 사용자 계정에 대 한 스키마의 일부인 데이터베이스 개체가 포함 됩니다. 사용자 계정 이름은 데이터 원본 속성 자격 증명에 지정되어 있습니다.  
  
### <a name="to-create-a-new-data-source-for-a-report-model-using-report-manager"></a>보고서 관리자를 사용하여 보고서 모델에 대한 새 데이터 원본을 만들려면  
  
1.  웹 브라우저의 주소 표시줄에 보고서 서버의 URL을 입력합니다.  
  
2.  **새 데이터 원본**을 클릭합니다.  
  
3.  **이름** 입력란에 데이터 원본의 이름을 입력합니다.  
  
4.  필요에 따라 **설명** 입력란에 모델에 대한 간략한 설명을 입력합니다.  
  
5.  **이 데이터 원본 사용** 확인란이 선택되어 있는지 확인합니다.  
  
6.  **연결 유형** 목록에서 연결할 데이터 원본 유형을 선택합니다. 연결 유형을 다음 중 하나 여야 합니다. **Oracle**하십시오 **Microsoft SQL Server** 하거나 **Microsoft SQL Server Analysis Services**합니다.  
  
7.  **연결 문자열** 입력란에 데이터베이스를 가리키는 연결 문자열을 입력합니다.  
  
8.  보고서 작성기 사용자가 데이터베이스에 연결할 때 사용할 연결 방법을 선택합니다.  
  
    -   Windows 인증: 운영 체제를 인증 하려는 경우이 옵션을 선택 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 사용자입니다. 이 옵션을 사용하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서는 암호 암호화 같은 Windows 보안 기능을 사용하여 사용자를 인증할 수 있습니다. 이 옵션을 반드시 선택하도록 합니다.  
  
    -   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증: 사용자가 사용 하도록 하려는 경우이 옵션을 선택는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 만든 로그인 계정입니다. 사용자는 유효한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로그인 이름과 암호를 제공해야 합니다.  
  
        > [!CAUTION]  
        >  가능하면 Windows 인증을 사용하십시오.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-create-a-report-model-using-report-manager"></a>보고서 관리자를 사용하여 보고서 모델을 만들려면  
  
1.  보고서 관리자에서 모델에 사용할 데이터 원본을 선택합니다.  
  
     속성 페이지가 표시됩니다.  
  
2.  데이터 원본에 대해 지정된 옵션을 사용할 것인지 확인합니다.  
  
3.  **모델 생성**을 클릭합니다.  
  
     데이터 원본에 대한 일반 페이지가 표시됩니다.  
  
4.  **이름** 입력란에 보고서 모델의 이름을 입력합니다.  
  
5.  **설명** 입력란에 모델에 대한 간단한 설명을 입력합니다.  
  
6.  보고서 모델을 저장할 새 위치를 지정하려면 **위치 변경**을 클릭합니다.  
  
     기본적으로 보고서 모델은 보고서 관리자 홈에 저장됩니다.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     보고서 모델이 생성되고 사용자가 지정한 위치에 저장됩니다. 보고서 관리자를 사용하여 이 모델에 대한 사용 권한을 할당할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [기본 모드 보고서 서버에 대한 사용 권한 부여](security/granting-permissions-on-a-native-mode-report-server.md)   
 [데이터 연결, 데이터 원본 및 Reporting Services의 연결 문자열](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [새 데이터 원본 페이지&#40;보고서 관리자&#41;](../../2014/reporting-services/new-data-source-page-report-manager.md)  
  
  
