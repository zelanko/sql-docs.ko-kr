---
title: Microsoft Access (Reporting Services)에서 보고서를 가져올 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Access reports [Reporting Services]
- importing reports
ms.assetid: 4f29d5b8-b77d-4714-a84a-05523df55646
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 862d8b90f3c91dffda35971677db7fdc231c1b63
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108924"
---
# <a name="import-reports-from-microsoft-access-reporting-services"></a>Microsoft Access에서 보고서 가져오기(Reporting Services)
  보고서 디자이너에서 보고서를 가져올 수 있습니다는 [!INCLUDE[msCoName](../includes/msconame-md.md)] Access 데이터베이스 또는 프로젝트입니다. 단, 보고서 디자이너가 설치되어 있는 컴퓨터에 Access 2002 이상이 설치되어 있어야 합니다.  
  
 가져오기 기능을 사용하면 데이터베이스나 프로젝트 파일의 모든 보고서를 가져옵니다. Access 파일에 보고서가 많이 있을 경우 보고서를 가져올 개별 보고서 프로젝트를 만든 후 주 보고서 프로젝트에서 각 RDL 파일을 열 수 있습니다. 보고서를 보고서 디자이너로 가져와야 편집할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 일부 Access 보고서 개체는 지원되지 않습니다. 변환 되지 않은 항목에 표시 됩니다는 **작업 목록** 창입니다. 자세한 내용은 [지원 되는 Access 보고서 기능 &#40;SSRS&#41;](../../2014/reporting-services/supported-access-report-features-ssrs.md)합니다.  
  
### <a name="to-import-reports-from-microsoft-access"></a>Microsoft Access에서 보고서를 가져오려면  
  
1.  보고서를 가져올 프로젝트를 열거나 만듭니다.  
  
2.  에 **프로젝트** 메뉴에서 **보고서 가져오기**를 클릭 하 고 **Microsoft Access**합니다. 또는 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭, 가리킨 **보고서 가져오기**를 클릭 하 고 **Microsoft Access**합니다.  
  
3.  에 **열기** 대화 상자에서 Access 데이터베이스 (.mdb,.accdb)을 선택 또는 프로젝트 (.adp) 보고서를 포함 하 고 클릭 **열기**합니다. 그러면 데이터베이스 또는 프로젝트 파일의 모든 보고서가 가져와지고 솔루션 탐색기의 보고서 폴더에 나열됩니다.  
  
4.  확인 합니다 **작업 목록** 창에서 빌드 오류입니다. 보려는 합니다 **작업 목록** 창을 열려면 합니다 **보기** 메뉴에서 **다른 Windows**, 클릭 하 고 **작업 목록**.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 디자이너로 보고서 디자인&#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  
  
