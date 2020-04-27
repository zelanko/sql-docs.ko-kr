---
title: 보기 페이지, 보고서 (보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4874ba29-429b-4dd4-a8cb-d4f087237dc2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c8731c1d0f79d99919c4a087521565a6ec590278
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66098737"
---
# <a name="view-page-reports-report-manager"></a>보기 페이지, 보고서(보고서 관리자)
  보고서의 보기 페이지를 사용하여 보고서를 볼 수 있습니다. 보고서 관리자에서 보고서를 처음 열면 HTML 형식으로 열립니다. HTML 보고서의 맨 위에는 보고서 도구 모음이 포함되어 있어서 보고서 페이지를 탐색하고 보고서 내에서 검색하거나 보고서를 다른 형식으로 내보내는 작업이 가능합니다. 다음 다이어그램에서는 보고서 도구 모음을 보여 줍니다.  
  
 ![보고서 도구 모음](media/htmlviewer-toolbar.gif "보고서 도구 모음")  
보고서 도구 모음  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서는 요청 시 실행되거나 보고서 실행 스냅샷에서 실행되도록 보고서를 구성할 수 있습니다. 보고서가 요청 시 실행되는 경우 보고서를 열 때마다 모든 데이터 및 보고서가 처리됩니다. 보고서 실행 스냅샷으로 실행되도록 구성된 보고서를 보는 경우 스냅샷을 만들 때 데이터가 처리됩니다.  
  
## <a name="exporting-reports"></a>보고서 내보내기  
 일부 보고서 기능은 일부 내보내기 형식에서 사용할 수 없습니다. HTML 보고서를 다른 형식으로 내보내는 경우 보고서 표시 방법이 서로 다를 수 있습니다. 또한 보고서에 하이퍼링크, 책갈피 또는 문서 구조 등의 대화형 기능이 있는 경우 새 형식에서는 이러한 기능을 사용할 수 없거나 동작 방식이 다를 수도 있습니다.  
  
## <a name="generating-data-feeds-from-report-data"></a>보고서 데이터에서 데이터 피드 생성  
 보고서에서 데이터 피드를 생성할 수 있습니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Atom 렌더링 확장 프로그램에서는 보고서가 제공하는 데이터 피드를 나열하는 Atom 서비스 문서와 보고서 데이터를 포함하는 데이터 피드의 두 가지 Atom 호환 문서를 생성합니다. 데이터 피드는 Atom 호환 데이터 피드를 사용하는 애플리케이션에서 읽고 교환할 수 있는 표준화된 Atom 1.0 호환 형식으로 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 에서 생성됩니다. 예를 들어 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 클라이언트는 보고서에서 생성된 데이터 피드를 사용할 수 있습니다.  
  
## <a name="running-parameterized-reports"></a>매개 변수 있는 보고서 실행  
 입력 필드 및 **보고서 보기** 단추를 포함하는 보고서를 매개 변수가 있는 보고서라고 합니다. 매개 변수가 있는 보고서를 보려면 보고서 실행에 사용되는 값을 제공해야 할 수도 있습니다.  
  
> [!NOTE]  
>  보고서 실행 스냅샷 및 일부 내보내기 형식은 일부 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 사용할 수 없습니다. 자세한 내용은 [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 관리자&#40;SSRS 기본 모드&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [보고서 관리자 F1 도움말](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
