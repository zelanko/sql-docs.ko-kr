---
title: 최대 파일 업로드 크기 (SharePoint 용 파워 피벗) 구성 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 15ce366acc4244db16f0b58bbdc8226e9327416c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34027230"
---
# <a name="configure-maximum-file-upload-size-power-pivot-for-sharepoint"></a>최대 파일 업로드 크기 구성(SharePoint용 파워 피벗)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서에 많은 데이터가 포함되어 SharePoint 업로드에 대해 허용되는 최대 파일 크기가 초과되는 경우가 많습니다. 이 상한을 초과하는 파일을 업로드하려고 하면 SharePoint에서  
  
-   “지정된 파일이 지원되는 최대 파일 크기보다 큽니다."라는 오류가 표시됩니다.  
  
 파일 크기를 늘리려면 먼저 Excel 서비스의 최대 통합 문서 크기를 50MB로 조정합니다. 그러면 Excel의 최대 파일 크기 제한이 SharePoint 웹 애플리케이션의 제한에 맞게 조정됩니다(SharePoint 2010에서는 기본적으로 50MB, SharePoint 2013에서는 200MB로 설정됨). 파일 크기가 50MB를 초과하는 경우 Excel 서비스와 웹 애플리케이션의 파일 크기 제한을 모두 높이십시오.  
  
 최대 파일 업로드 크기를 변경하려면 SharePoint 관리자여야 합니다.  
  
### <a name="configure-maximum-file-size-for-excel-services"></a>Excel 서비스의 최대 파일 크기 구성  
  
1.  중앙 관리의 애플리케이션 관리에서 **서비스 애플리케이션 관리**를 클릭합니다.  
  
2.  Excel 서비스 애플리케이션의 이름을 클릭합니다.  
  
3.  **신뢰할 수 있는 파일 위치**를 클릭합니다.  
  
4.  속성을 편집할 위치를 클릭합니다. 기본적으로 Excel 서비스는 기본 웹 애플리케이션을 신뢰할 수 있는 사이트로 간주합니다. 기본 웹 애플리케이션을 사용 중인 경우 **http://** 를 클릭하여 해당 위치의 구성 페이지를 엽니다.  
  
5.  **통합 문서 속성**으로 스크롤합니다.  
  
6.  최대 통합 문서 크기에서 파일 크기를 10(기본값)에서 50 또는 작업 중인 파일에 맞는 더 큰 값으로 늘립니다.  
  
     기본적으로 SharePoint 웹 애플리케이션의 최대 파일 업로드 크기는 50MB입니다. 최대 통합 문서 크기를 50MB보다 더 크게 설정하는 경우에는 다음 절차의 단계에 따라 SharePoint 웹 애플리케이션의 최대 업로드 크기도 같은 값으로 늘립니다.  
  
     지정할 수 있는 최대 값은 2GB(또는 중앙 관리에 지정된 대로 2047MB)입니다.  
  
7.  **확인**을 클릭합니다.  
  
### <a name="configure-maximum-file-size-for-a-sharepoint-web-application"></a>SharePoint 웹 애플리케이션의 최대 파일 크기 구성  
  
1.  중앙 관리의 애플리케이션 관리에서 **웹 애플리케이션 관리**를 클릭합니다.  
  
    > [!NOTE]  
    >  Excel 서비스의 최대 통합 문서 크기를 증가시킨 경우에만 다음 단계를 수행합니다.  
  
2.  애플리케이션(예: **SharePoint -80**)을 선택합니다.  
  
3.  웹 애플리케이션 리본의 일반 설정 단추에서 아래쪽 화살표를 클릭합니다.  
  
4.  **일반 설정**을 클릭합니다.  
  
5.  **최대 업로드 크기**로 스크롤합니다.  
  
6.  속성을 Excel 서비스의 최대 통합 문서 크기와 같은 값 또는 더 큰 값으로 설정합니다.  
  
7.  **확인**을 클릭합니다.  
  
  
