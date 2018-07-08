---
title: 보고서에서 데이터 피드 생성(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e68baae2-9f2a-4f13-9179-9ac7f29111c5
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 4ee1402202e08ab4ba718238b454f5eb4e548118
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37210833"
---
# <a name="generate-data-feeds-from-a-report-report-builder-and-ssrs"></a>보고서에서 데이터 피드 생성(보고서 작성기 및 SSRS)
  보고서에서 Atom 규격 데이터 피드를 생성 하 고 다음 데이터 피드는 응용 프로그램에서 같은 사용할 수 있습니다 합니다 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 피드를 사용할 수 있는 클라이언트입니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Atom 렌더링 확장 프로그램은 보고서에서 사용할 수 있는 데이터 피드를 나열하는 Atom 서비스 문서를 생성합니다. 이 문서는 보고서의 각 데이터 영역에 대한 데이터 피드를 하나 이상 나열합니다. 데이터 영역의 유형과 데이터 영역에 표시되는 데이터에 따라 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 데이터 영역에서 여러 데이터 피드를 생성할 수 있습니다.  
  
 Atom 서비스 문서에는 각 데이터 피드에 대한 고유 식별자가 포함되며 URL에서 이 식별자를 사용하여 데이터 피드의 내용을 볼 수 있습니다.  
  
 자세한 내용은 [보고서에서 데이터 피드 생성&#40;보고서 작성기 및 SSRS&#41;](generating-data-feeds-from-reports-report-builder-and-ssrs.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-generate-an-atom-service-document"></a>Atom 서비스 문서를 생성하려면  
  
1.  보고서 관리자 **홈** 페이지에서 데이터 피드를 생성할 보고서를 찾아 이동합니다.  
  
2.  보고서를 클릭합니다.  
  
     보고서가 실행됩니다.  
  
3.  도구 모음에서 데이터 피드로 내보내기 아이콘을 클릭합니다.  
  
     데이터 피드가 포함된 Atom 문서를 저장하거나 열지 확인하는 메시지가 나타납니다.  
  
4.  **저장** 을 클릭하여 파일 시스템에 문서를 저장하거나 저장하기 전에 **열기** 를 클릭하여 문서 내용을 봅니다. **기본적으로 브라우저에서 문서가 열립니다.**  
  
5.  문서를 저장할 위치를 찾습니다.  
  
6.  필요한 경우 문서 이름을 변경합니다.  
  
    > [!NOTE]  
    >  기본적으로 문서 이름은 보고서 이름입니다.  
  
7.  문서 유형이 **ATOMSVC 파일**인지 확인한 다음 **저장**을 클릭합니다.  
  
8.  필요한 경우 브라우저, 텍스트 편집기 또는 XML 편집기에서 .atomsvc 파일을 엽니다.  
  
### <a name="to-view-an-atom-compliant-data-feed"></a>Atom 규격 데이터 피드를 보려면  
  
1.  Atom 서비스 문서가 열려 있지 않으면 해당 문서를 찾아 Internet Explorer와 같은 브라우저에서 엽니다.  
  
2.  Atom 서비스 문서에서 보려는 데이터 피드의 URL을 브라우저에 복사합니다.  
  
     URL 형식은 다음과 같습니다.  
  
 `http://<server name>/ReportServer?%2f<ReportName>rs%3aCommand=Render&rs%3aFormat=ATOM&rc%3aDataFeed=<Identifier>`  
  
1.  Enter 키를 누릅니다.  
  
     데이터 피드가 포함된 Atom 문서를 저장하거나 열지 확인하는 메시지가 나타납니다.  
  
2.  **저장** 을 클릭하여 파일 시스템에 문서를 저장하거나 저장하기 전에 **열기** 를 클릭하여 데이터 피드를 봅니다.  
  
3.  문서를 저장할 위치를 찾습니다.  
  
4.  필요한 경우 문서 이름을 변경합니다.  
  
    > [!NOTE]  
    >  기본적으로 문서 이름은 보고서 이름입니다. Atom 서비스 문서에 피드가 여러 개 있으면 기본적으로 모든 피드가 같은 이름인 보고서 이름을 사용합니다. 피드를 구별하려면 피드 이름을 의미 있는 이름으로 바꿉니다.  
  
5.  문서 유형이 **ATOM 파일**인지 확인한 다음 **저장**을 클릭합니다.  
  
6.  필요한 경우 브라우저, 텍스트 편집기 또는 XML 편집기에서 .atom 파일을 엽니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서를 내보내는 &#40;보고서 작성기 및 SSRS&#41;](export-reports-report-builder-and-ssrs.md)  
  
  
