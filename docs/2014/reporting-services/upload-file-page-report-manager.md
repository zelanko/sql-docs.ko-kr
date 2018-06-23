---
title: 파일 업로드 페이지 (보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7bb3166f-9374-4449-b66a-ffb77298507d
caps.latest.revision: 27
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 5cdc35c029b40489e43e8e8b5715846cdab1fa6a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36183745"
---
# <a name="upload-file-page-report-manager"></a>파일 업로드 페이지(보고서 관리자)
  파일 업로드 페이지를 사용하여 파일을 파일 시스템에서 보고서 서버 데이터베이스로 게시할 수 있습니다. 업로드된 파일은 보고서 서버 폴더 계층 구조의 항목으로 표시됩니다.  
  
-   업로드된 .rdl 파일은 보고서 서버에 보고서로 게시됩니다.  
  
-   Uploaded .smdl 파일이 데이터 원본 뷰 정보를 포함하는 경우 이 파일은 보고서 모델로 게시됩니다. 데이터 원본 뷰 참조가 유실되면 업로드 중에 오류가 발생합니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 보고서 모델 프로젝트에서 .smdl 파일을 업로드하면 데이터 원본 뷰 정보가 누락될 수 있습니다. 보고서 모델 프로젝트에서 데이터 원본 뷰 정보는 .smdl 파일 자체가 아닌 별도의 파일에 저장됩니다.  
  
     데이터 원본 뷰 정보가 들어 있고 따라서 성공적으로 업로드할 수 있는 모델 파일은 이전에 보고서 서버에 게시된 후 서버에서 파일 시스템의 파일로 저장된 파일입니다. 모델의 일반 속성 페이지를 열고 **편집** 을 클릭하여 모델을 연 경우 파일에 모델을 저장하고 보고서 서버에 새 모델로 해당 파일을 업로드할 수 있습니다. 나중에 업로드하는 .smdl 파일은 모델 게시에 필요한 모든 정보를 포함하게 됩니다.  
  
-   다른 모든 업로드한 파일 형식은 리소스로 저장됩니다. 여기에는 보고서 데이터 원본 연결 정보가 있는 .rds 파일이 포함됩니다. .rds 파일을 업로드해도 보고서 서버에 공유 데이터 원본 항목이 생성되지 않습니다.  
  
 항목을 업로드하면 이 항목은 현재 폴더에 놓입니다. 업로드가 완료된 후 항목을 다른 위치로 이동할 수 있습니다.  
  
> [!NOTE]  
>  이 기능은 일부 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]버전에서는 사용할 수 없습니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], 참조 [SQL Server 2014 버전에서 지 원하는 기능](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다.  
  
## <a name="navigation"></a>탐색  
 사용자 인터페이스(UI)에서 이 위치를 탐색하려면 다음 절차를 사용하십시오.  
  
### <a name="to-open-the-upload-file-page"></a>파일 업로드 페이지를 열려면  
  
1.  보고서 관리자를 열고 파일을 업로드할 폴더로 이동합니다.  
  
2.  도구 모음에서 **파일 업로드**를 클릭합니다.  
  
## <a name="options"></a>변수  
 **업로드할 파일**  
 파일 시스템에서 복사할 파일의 정규화된 경로를 표시합니다.  
  
 **찾아보기**  
 파일 시스템에서 파일을 선택하려면 클릭합니다.  
  
 **이름**  
 보고서 서버 네임스페이스에 표시될 파일 이름을 입력합니다. 이름은 하나 이상의 영숫자 문자를 포함해야 합니다. 공백과 특정 기호도 포함할 수 있습니다. 이름을 지정할 때 ; ? : @ & = +, $ * \< > | "또는 / 항목 이름을 지정 하는 경우.  
  
 **항목이 있으면 덮어쓰기**  
 기존 항목을 새 버전으로 교체하려면 이 확인란을 선택합니다. 기존 버전을 덮어쓰려면 새 항목과 기존 항목의 이름이 정확히 일치해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 관리자 &#40;SSRS 기본 모드&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [페이지 콘텐츠 &#40;보고서 관리자&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [보고서 관리자 F1 도움말](../../2014/reporting-services/report-manager-f1-help.md)   
 [폴더에 파일 업로드](report-server/upload-files-to-a-folder.md)  
  
  