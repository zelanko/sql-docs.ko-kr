---
title: 보고서 파트 게시 및 다시 게시(보고서 작성기) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 92dce484-f39b-403c-9caf-d8772bc3aca3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2ea76e42cb7230bc4195cc8c2dc1615308fa4058
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77082353"
---
# <a name="publish-and-republish-report-parts-report-builder-and-ssrs"></a>보고서 파트 게시 및 다시 게시(보고서 작성기 및 SSRS)
  보고서 파트는 보고서 서버에 별도로 게시된 페이지를 매긴 보고서 항목으로, 다른 페이지를 매긴 보고서에서 다시 사용할 수 있습니다. 보고서 파트는 기본 설정으로 기본 위치에 게시할 수도 있고 이름, 설명 등의 보고서 파트 메타데이터를 편집한 다음 보고서 서버의 다른 위치에 저장할 수도 있습니다. 또한 올바른 권한이 있는 경우에는 보고서 서버와 통합된 SharePoint 사이트에 보고서 파트를 저장할 수도 있습니다.  
  
 보고서 파트가 사용하는 데이터 세트를 포함하여 보고서 파트만 게시하거나 데이터 세트를 별도로 게시할 수 있습니다. 데이터 세트를 별도로 게시하는 경우에는 공유 데이터 세트가 되며 보고서 파트가 이 데이터 세트에 연결됩니다. 자세한 내용은 [보고서 작성기의 보고서 파트 및 데이터 세트](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)를 참조하세요.  
  
 기존 보고서 파트를 다시 게시할 수도 있습니다. 권한이 있는 경우에는 서버에 있는 보고서 파트(자신이 만든 것이 아니어도 됨)의 원본 인스턴스를 덮어써 저장할 수도 있습니다. 또한 새 보고서 파트로 게시한 다음 같은 위치나 다른 위치에 저장할 수도 있습니다.  
  
## <a name="to-publish-a-report-part"></a>보고서 파트를 게시하려면  
  
1.  보고서 작성기 메뉴에서 **보고서 파트 게시**를 클릭합니다.  
  
     보고서 서버에 연결되어 있지 않은 경우에는 연결하라는 메시지가 표시됩니다. 보고서 서버에 연결할 수 없으면 보고서 파트를 게시할 수 없습니다.  
  
2.  보고서 파트를 기본 설정으로 기본 위치에 저장하려면 **모든 보고서 파트를 기본 설정으로 게시**를 클릭합니다.  
  
     그렇지 않으면 **게시하기 전에 보고서 파트 검토 및 수정**을 클릭합니다.  
  
3.  보고서 파트 이름 및 설명을 편집하려면 이름을 두 번 클릭해 편집하고 **설명** 필드를 클릭해 설명을 추가합니다.  
  
    > [!NOTE]  
    >  다른 사람들이 검색할 때 쉽게 식별할 수 있도록 명확한 보고서 파트 이름과 설명을 지정하는 것이 좋습니다. 보고서 파트 이름의 최대 길이는 260자(전체 경로)입니다. 여기에는 서버의 폴더 이름 뒤에 보고서 파트의 실제 이름이 붙습니다.  
  
4.  보고서 파트를 기본 폴더가 아닌 다른 폴더에 저장하려면 **찾아보기** 단추를 클릭합니다.  
  
5.  보고서의 모든 보고서 파트에 대한 옵션을 설정했으면 **게시**를 클릭합니다.  
  
     보고서 파트를 게시하고 나면 대화 상자에 제대로 게시된 항목과 그렇지 않은 항목이 표시됩니다. **보고서 파트 게시** 대화 상자에서 게시되지 않은 보고서 파트에 대한 상세 정보를 확인할 수 있습니다.  
  
6.  **닫기**를 클릭합니다.  
  
## <a name="to-republish-a-report-part"></a>보고서 파트를 다시 게시하려면  
  
1.  이전 절차에 따라 보고서 파트를 게시합니다.  
  
2.  **보고서 파트 게시** 대화 상자에서 **보고서 항목의 새 복사본으로 게시**를 클릭하면 보고서 작성기에서 서버의 기존 보고서 파트를 덮어써 저장하지 않고 다른 보고서 파트를 만듭니다.  
  
> [!NOTE]  
>  새 보고서 파트로 게시하는 경우에는 새 고유 ID가 지정되며 원본 보고서 파트를 변경해도 더 이상 업데이트를 받지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 파트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)   
 [보고서 작성기의 보고서 파트 및 데이터 세트](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)   
 [보고서 파트 문제 해결(보고서 작성기 및 SSRS)](https://msdn.microsoft.com/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [업데이트 확인 또는 업데이트 해제(보고서 작성기 및 SSRS)](https://msdn.microsoft.com/9c69792d-d7c4-453b-ae2f-6d2d071d8606)   
 [보고서 파트 찾아보기 및 기본 폴더 설정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md)  
  
  
