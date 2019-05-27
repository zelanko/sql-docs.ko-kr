---
title: 보고서 파트 (보고서 작성기 및 SSRS) 문제 해결 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d9fe1932-46e7-421b-a8a9-4c54d9576e94
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: df37de909461ace62edbbf3cfe9e7b9dd8448b56
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66099386"
---
# <a name="troubleshoot-report-parts-report-builder-and-ssrs"></a>보고서 파트 문제 해결(보고서 작성기 및 SSRS)
  다음은 보고서 파트로 작업할 때 도움이 되는 정보입니다  
  
## <a name="why-do-my-co-worker-and-i-see-different-instances-of-the-same-report-part-when-we-search-for-it"></a>사용자와 사용자의 동료가 보고서 파트를 검색할 때 동일한 보고서 파트의 서로 다른 인스턴스가 표시되는 이유는 무엇입니까?  
 보고서 서버 또는 보고서 서버와 통합된 SharePoint 사이트에는 단일 보고서 파트의 여러 인스턴스가 있을 수 있으며, 이 경우 모든 인스턴스의 GUID(Globally Unique Identifier)는 동일합니다. 최신 인스턴스만 검색 결과의 목록에 표시됩니다. 단일 보고서 파트의 여러 인스턴스에 대한 사용 권한이 서로 다른 경우가 있습니다. 사용자와 사용자의 동료가 서버에서 서로 다른 사용 권한을 갖고 있는 경우 동일한 인스턴스를 보지 못합니다. 예를 들어 모두 GUID가 같은 보고서 파트의 여러 복사본을 SharePoint 통합 모드에서 보고서 서버의 각각 다른 폴더에 저장하는 경우 이들 폴더의 사용 권한이 다르면 해당 폴더에 있는 보고서 파트의 사용 권한도 각각 다릅니다.  
  
 사용자와 사용자의 동료가 갖고 있는 사용 권한을 보려면 보고서 서버 관리자에게 문의하십시오.  
  
## <a name="when-i-search-for-report-parts-that-i-uploaded-to-a-sharepoint-server-i-do-not-see-them-why-not"></a>SharePoint 서버로 업로드한 보고서 파트가 검색되지 않는 이유는 무엇입니까?  
 보고서 작성기를 사용하여 게시하는 대신 SharePoint 문서 라이브러리로 수동 업로드한 보고서 파트는 보고서 파트 갤러리에 표시되지 않을 수 있습니다. 갤러리 검색에 사용되는 보고서 서버를 SharePoint 문서 라이브러리의 내용과 동기화해야 할 수 있습니다. 자세한 내용은 [SharePoint 중앙 관리에서 보고서 서버 파일 동기화 기능 활성화](../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md) 에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [온라인](https://go.microsoft.com/fwlink/?LinkId=154888) msdn.microsoft.com 합니다.  
  
## <a name="why-cant-others-see-the-image-in-their-reports"></a>다른 사용자가 자신의 보고서에서 이미지를 볼 수 없는 이유는 무엇입니까?  
 이미지 파일에 대한 링크인 보고서 파트를 게시하는 경우 해당 보고서 파트는 실제로 링크일 뿐입니다. 다른 사용자가 이미지 보고서 파트를 자신의 보고서에 추가할 때 이미지를 볼 수 없는 경우 연결되어 있는 이미지에 대한 사용 권한이 없을 수 있습니다.  
  
 이 문제를 해결할 수 있는 몇 가지 방법이 있습니다.  
  
-   이미지 파일에 대한 링크를 보고서 파트로 만드는 대신 이미지 파일을 보고서 파트로 만듭니다.  
  
-   이미지 파일을 다른 사용자가 사용 권한을 가진 위치로 이동합니다.  
  
-   사용 권한을 변경하려면 보고서 서버 관리자에게 문의하십시오.  
  
## <a name="why-do-i-get-a-circular-reference-error-message-when-i-try-to-publish-my-report-part"></a>보고서 파트를 게시하려고 하면 “순환 참조” 오류 메시지가 표시되는 이유는 무엇입니까?  
 순환 참조가 포함된 보고서 항목은 보고서 파트로 게시할 수 없습니다. 예를 들어 보고서 항목이 가리키는 데이터 집합이 매개 변수를 가리키고 이 매개 변수가 데이터 집합을 다시 가리킬 수 있습니다. 이 경우에는 참조 중 하나를 삭제해야 보고서 파트를 게시할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 파트&#40;보고서 작성기 및 SSRS&#41;](report-parts-report-builder-and-ssrs.md)  
  
  
