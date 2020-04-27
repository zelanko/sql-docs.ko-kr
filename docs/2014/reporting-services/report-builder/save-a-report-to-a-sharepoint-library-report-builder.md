---
title: SharePoint 라이브러리에 보고서 저장(보고서 작성기) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4daa1eee-78b7-43d0-8b22-4a98e8fa66ba
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ab4f9b06758d29ff1f988f37b95ce92206f34d39
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66107683"
---
# <a name="save-a-report-to-a-sharepoint-library-report-builder"></a>SharePoint 라이브러리에 보고서 저장(보고서 작성기)
  SharePoint 통합용으로 구성된 보고서 서버에 보고서를 저장하려면 SharePoint 서버로 이동하여 보고서 서버에 대한 연결을 설정해야 합니다. 보고서 정의에서 보고서와 관련된 항목에 대한 모든 참조에는 SharePoint 보고서 서버에 맞는 값을 사용해야 합니다. 관련 항목에는 하위 보고서, 드릴스루 보고서 및 웹 기반 이미지 등의 리소스가 포함됩니다. 자세한 내용은 [외부 항목에 대한 경로 지정&#40;보고서 작성기 및 SSRS&#41;](../report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md)을 참조하세요.  
  
 프로젝트의 속성을 설정하려면 SharePoint 사이트에 대한 **멤버** 또는 **소유자** 권한이 있어야 합니다.  
  
### <a name="to-save-a-report-to-a-sharepoint-site"></a>SharePoint 사이트에 보고서를 저장하려면  
  
1.  보고서 작성기 단추에서 **저장**을 클릭합니다. _\<보고서 항목>_ **로 저장**대화 상자가 열립니다.  
  
    > [!NOTE]  
    >  보고서를 다시 저장하는 경우 보고서가 이전 위치에 자동으로 다시 저장됩니다. **다른 이름으로 저장** 옵션을 사용하여 위치를 변경할 수 있습니다.  
  
2.  필요한 경우 **최근에 사용한 사이트 및 서버** 를 클릭하여 최근에 사용한 보고서 서버와 SharePoint 사이트의 목록을 표시합니다.  
  
3.  SharePoint 사이트를 찾은 다음 **저장**을 클릭합니다.  
  
    > [!NOTE]  
    >  변경된 보고서를 저장하지 않은 상태로 10시간 이상 두면 저장되지 않은 상태로 서버에서 연결이 끊어집니다. 그러면 왼쪽 아래의 상태 표시줄에서 **연결 끊기**를 클릭한 다음 **연결**을 클릭합니다. 최신 서버는 사용 가능한 서버 목록에 있습니다. 서버를 선택하면 보고서가 다시 연결됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 찾기, 보기 및 관리&#40;보고서 작성기 및 SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
