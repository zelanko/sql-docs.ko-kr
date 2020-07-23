---
title: 폴더 속성 대화 상자 | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.isfolderprop.permissions.f1
- sql13.ssis.ssms.iscreatefolder.f1
- sql13.ssis.ssms.isfolderprop.general.f1
ms.assetid: d9a2bfae-fcc8-46be-b588-4a9db03f7e45
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 334105bde7936543fd1dba3167fd61e1b440fd5e
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86922649"
---
# <a name="folder-properties-dialog-box"></a>폴더 속성 대화 상자

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  폴더에는 **SSISDB** 카탈로그의 프로젝트 및 환경이 포함됩니다. 각 폴더는 폴더 내용에 적용되는 사용 권한을 정의합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 권한에 대한 자세한 내용은 [catalog.grant_permission&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database.md)을 참조하세요.  
  
## <a name="to-set-folder-description-and-permissions"></a>폴더 설명 및 사용 권한을 설정 하려면  
  
1.  해당 폴더를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
2.  **일반** 페이지의 **일반** 아래에서 **설명** 을 선택하고 선택적인 설명을 입력합니다.  
  
3.  **사용 권한** 페이지에서 **찾아보기...** 를 클릭하고 하나 이상의 데이터베이스 보안 주체를 선택하고 **확인**을 클릭합니다.  
  
4.  **로그인 또는 역할** 아래에서 이름을 선택하고 **사용 권한**아래에서 적합한 권한을 지정합니다.  
  
5.  **확인** 을 클릭하여 변경 사항을 수락하고 **폴더 속성** 대화 상자를 닫습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services &#40;SSIS&#41; 서버](../integration-services-ssis-packages.md)   
 [catalog.grant_permission &#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database.md)  
  
  
