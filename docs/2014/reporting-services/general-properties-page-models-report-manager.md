---
title: 일반 속성 페이지, 모델 (보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.modelproperties.general.f1
ms.assetid: 7ad59850-8135-4c4d-95e9-6d705b6d77a8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 3f3756fb68ba46b1ac7b34237753dbd57d0b6775
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48146253"
---
# <a name="general-properties-page-models-report-manager"></a>일반 속성 페이지, 모델(보고서 관리자)
  보고서 모델의 일반 속성 페이지를 사용하여 모델 정의 파일(.smdl)의 이름을 바꾸거나 파일을 삭제, 이동 또는 대체할 수 있습니다. 모델을 만들거나 수정한 사람 및 변경된 시간에 대한 자세한 내용은 페이지 맨 위에 표시됩니다.  
  
## <a name="navigation"></a>탐색  
 사용자 인터페이스(UI)에서 이 위치를 탐색하려면 다음 절차를 사용하십시오.  
  
###### <a name="to-open-the-general-properties-page-for-a-model"></a>모델의 일반 속성 페이지를 열려면  
  
1.  보고서 관리자를 열고 속성을 보거나 구성하려는 모델을 찾습니다.  
  
2.  모델 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
3.  드롭다운 메뉴에서 **관리**를 클릭합니다. 모델의 일반 속성 페이지가 열립니다.  
  
## <a name="options"></a>변수  
 **이름**  
 모델의 이름을 지정합니다. 이름은 하나 이상의 영숫자 문자를 포함해야 합니다. 공백과 특정 기호도 포함할 수 있습니다. 이름 지정 시에는 다음 문자를 사용하지 마십시오.  
  
 ; ? : \@ & = +, $ / * \< > | " /  
  
 **설명**  
 모델에 대한 설명을 입력합니다. 이 설명은 해당 모델 액세스 권한이 있는 사용자의 내용 페이지에 표시됩니다.  
  
 **목록 뷰에서 숨기기**  
 폴더의 뷰 모드가 목록 뷰인 경우 항목을 숨기려면 이 확인란을 선택합니다. 목록 뷰는 보고서 관리자에서 지원되는 폴더 내용을 보기 위한 모드입니다. 이 옵션을 설정할 수 있습니다 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 이 항목을 보고서 관리자에서가 표시 하는 방법을 정의 합니다. 보기 모드에서 보고서 관리자에 대 한 자세한 내용은 참조 하세요. [콘텐츠 페이지 &#40;보고서 관리자&#41;](../../2014/reporting-services/contents-page-report-manager.md)합니다.  
  
 **적용**  
 클릭하여 변경 내용을 저장합니다.  
  
 **Delete**  
 클릭하여 보고서 서버 데이터베이스에서 모델을 제거합니다. 모델을 삭제해도 연결 정보를 제공하는 종속 공유 데이터 원본과 해당 모델을 데이터 원본으로 사용하는 보고서는 삭제되지 않습니다. 단, 모델이 삭제된 후 해당 모델을 사용하는 보고서는 더 이상 실행되지 않습니다.  
  
 **이동**  
 클릭하여 보고서 서버 폴더 계층 구조 내의 다른 위치로 모델을 옮깁니다. 이 단추를 클릭하면 폴더를 검색하여 새 폴더 위치를 찾을 수 있는 항목 이동 페이지가 열립니다. 자세한 내용은 [항목 이동 페이지 &#40;보고서 관리자&#41;](../../2014/reporting-services/move-items-page-report-manager.md)합니다.  
  
 **저장**  
 모델 정의의 읽기 전용 복사본을 저장하려면 클릭합니다. 컴퓨터에 정의된 파일 연결에 따라 파일이 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 또는 다른 애플리케이션에서 열립니다. 대부분의 경우 모델은 XML 파일로 열립니다.  
  
 사용자가 여는 복사본은 보고서 서버에 초기에 게시된 원래 모델 정의와 동일합니다. 모델이 게시된 후 모델에 설정된 모든 속성(예: 데이터 원본 속성)은 여는 파일에 반영되지 않습니다.  
  
 모델 정의를 수정하고 공유 폴더에 새 파일로 저장한 다음 보고서 서버에 새 항목으로 업로드할 수 있습니다. 열려 있는 동안에 모델 정의를 확인 하는 수정 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] (또는 다른 응용 프로그램) 보고서 서버에 직접 저장 되지 않습니다. 수정한 모델을 보고서 서버에 게시하려면 해당 파일을 업로드해야 합니다.  
  
 모델 디자이너에서 보고서 모델을 열려면 모델을 .smdl 파일로 저장한 다음 이 .smdl 파일을 모델 디자이너의 프로젝트에 추가해야 합니다.  
  
 **바꾸기**  
 파일 시스템의 .smdl 파일에 있는 다른 정의로 모델 정의를 대체하려면 클릭합니다. 모델 정의를 업데이트하는 경우에는 업데이트를 완료한 후 공유 데이터 원본 설정을 다시 설정해야 합니다.  
  
 **모델 다시 생성**  
 클릭하여 현재 버전을 대체하는 기본 모델을 다시 생성합니다. 이 옵션은 모델이 생성된 후에 나타납니다. 생성된 모델은 공유 데이터 원본을 기반으로 합니다. 모델을 사용자 지정하려면 먼저 생성해야 합니다. 모델을 생성한 후에는 **편집** 을 클릭하여 모델 정의를 열고 파일 시스템에 이를 저장한 다음 모델 디자이너의 프로젝트에 추가할 수 있습니다. 모델을 구체화한 후에는 보고서 서버에 새 항목으로 업로드하거나 이 페이지의 **업데이트** 를 클릭하여 모델 디자이너에서 수정한 버전으로 생성된 버전을 대체할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [공유 데이터 원본을 보고서 또는 모델을 바인딩할 &#40;SSRS&#41;](report-data/bind-a-report-or-model-to-a-shared-data-source-ssrs.md)   
 [Management Studio의 보고서 서버 F1 도움말](tools/report-server-in-management-studio-f1-help.md)  
  
  
