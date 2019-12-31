---
title: 중앙 관리에서 PowerPivot 사이트에 대 한 신뢰할 수 있는 위치 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a666f365-cd93-43a3-9d3d-e429dfc19b66
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6c5dd66b72ff280431d29ae292af8fa1402095dc
ms.sourcegitcommit: 7183735e38dd94aa3b9bab2b73ccab54c916ff86
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2019
ms.locfileid: "74684090"
---
# <a name="create-a-trusted-location-for-powerpivot-sites-in-central-administration"></a>Create a trusted location for PowerPivot sites in Central Administration
  Excel 서비스에서는 SharePoint 서버에서 연 통합 문서에 올바른 리포지토리인 위치를 지정할 수 있습니다. 이러한 위치를 '신뢰할 수 있는 위치'라고 하며 사용자가 만든 신뢰할 수 있는 위치 각각에 대해 다른 구성 설정을 사용할 수 있습니다. SharePoint용 PowerPivot을 배포하는 경우 팜의 나머지 부분에는 기본 설정을 계속 사용하면서 PowerPivot 데이터 액세스에 가장 적합한 설정을 적용할 수 있도록 PowerPivot 통합 문서를 포함하는 사이트에 대한 신뢰할 수 있는 위치를 만드는 것을 고려할 수 있습니다.  
  
  
  
## <a name="prerequisites"></a>필수 구성 요소  
 URL을 신뢰할 수 있는 위치로 지정하려면 팜이나 서비스 관리자여야 합니다.  
  
 PowerPivot 갤러리나 통합 문서를 저장하는 기타 라이브러리를 포함하는 SharePoint 사이트의 URL 주소를 알아야 합니다. 주소를 가져오려면 라이브러리가 포함 된 사이트를 열고 **PowerPivot 갤러리**를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택한 다음 서버 이름과 사이트 경로가 포함 된 주소 (URL)의 첫 부분을 복사 합니다.  
  
##  <a name="overview"></a>설명은  
 Excel 서비스의 초기 설치에서는 'http://'를 해당하는 신뢰할 수 있는 위치로 지정합니다. 이는 팜에 있는 모든 사이트의 통합 문서가 서버에서 열릴 수 있음을 의미합니다. 신뢰할 수 있는 위치를 더 엄격하게 제어해야 하는 경우 팜에서 특정 사이트에 매핑되는 신뢰할 수 있는 위치를 새로 만든 다음 각 위치에 대해 설정 및 권한을 구성할 수 있습니다.  
  
 PowerPivot 통합 문서를 호스팅하는 사이트에 대해 신뢰할 수 있는 위치를 새로 만들면 팜의 나머지 부분에는 기본값을 계속 사용하면서 PowerPivot 데이터 액세스에 가장 적합한 서로 다른 설정을 적용하려는 경우 특히 유용합니다. 예를 들어 PowerPivot 통합 문서에 대해 최적화된 신뢰할 수 있는 위치에는 50MB의 최대 통합 문서 크기를 사용하고, 팜의 나머지 부분에는 10MB의 기본값을 그대로 사용합니다.  
  
 PowerPivot 갤러리 라이브러리를 사용하여 게시된 통합 문서를 미리 볼 때 원하는 미리 보기 이미지가 표시되지 않고 데이터 새로 고침 경고가 표시되는 경우에는 신뢰할 수 있는 위치를 만드는 것이 좋습니다. PowerPivot 갤러리는 문서 내의 데이터와 표시 정보를 사용하여 보고서와 통합 문서의 축소판 이미지를 렌더링합니다. 신뢰할 수 있는 위치에 대해 새로 고칠 때 경고가 설정되어 있는 경우 PowerPivot 갤러리에 새로 고침을 수행할 권한이 충분하지 않아 축소판 이미지 대신 오류가 표시될 수 있습니다. PowerPivot 갤러리를 포함하는 사이트를 새 신뢰할 수 있는 위치로 추가하여 이 문제를 해결할 수 있습니다.  
  
##  <a name="create"></a>PowerPivot 데이터 액세스를 위한 신뢰할 수 있는 위치 만들기  
  
1.  중앙 관리의 응용 프로그램 관리에서 **서비스 응용 프로그램 관리**를 클릭 합니다.  
  
2.  Excel Services 애플리케이션을 클릭합니다.  
  
3.  
  **신뢰할 수 있는 파일 위치**를 클릭합니다.  
  
4.  
  **신뢰할 수 있는 파일 위치 추가**를 클릭합니다.  
  
5.  PowerPivot 갤러리 라이브러리가 포함된 사이트의 URL을 입력합니다.  
  
6.  위치 유형에서 **Microsoft SharePoint Foundation**을 선택합니다.  
  
    > [!IMPORTANT]  
    >  UNC 및 HTTP 위치 유형은 PowerPivot 데이터 액세스에 지원되지 않습니다.  
  
7.  세션 관리, 통합 문서 속성 및 계산 동작 속성의 모든 기본 설정을 그대로 사용합니다.  
  
8.  통합 문서 속성에서 **최대 통합 문서 크기** 를 **50**으로 설정합니다. 그러면 통합 문서 파일 크기의 상한이 부모 웹 애플리케이션에 대한 파일 업로드 상한에 맞게 조정됩니다. 통합 문서가 50MB보다 크면 파일 크기 제한을 더 높여야 합니다. 자세한 내용은 [SharePoint용 PowerPivot&#41;&#40;최대 파일 업로드 크기 구성 ](configure-maximum-file-upload-size-power-pivot-for-sharepoint.md)을 참조 하세요.  
  
9. 외부 데이터에서 외부 데이터 허용이 **신뢰할 수 있는 데이터 연결 라이브러리 및 포함 라이브러리**로 설정되어 있는지 확인합니다. 통합 문서에서 PowerPivot 데이터에 액세스하려면 이 설정을 사용해야 합니다.  
  
10. 외부 데이터에서 새로 고칠 때 경고에 대한 **새로 고침 경고 사용**확인란의 선택을 취소합니다. 이 확인란 선택을 취소하면 PowerPivot 갤러리가 루틴 경고 메시지를 무시하고 대신 통합 문서의 미리 보기 이미지를 표시할 수 있습니다.  
  
11. 
  **확인**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [PowerPivot 갤러리](../../2014-toc/index.yml)  
 [PowerPivot 갤러리 만들기 및 사용자 지정](create-and-customize-power-pivot-gallery.md)   
 [PowerPivot 갤러리 사용](use-power-pivot-gallery.md)  
  
  
