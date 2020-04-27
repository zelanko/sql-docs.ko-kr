---
title: Microsoft Access에서 보고서 가져오기 (Reporting Services) | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108924"
---
# <a name="import-reports-from-microsoft-access-reporting-services"></a>Microsoft Access에서 보고서 가져오기(Reporting Services)
  보고서 디자이너 [!INCLUDE[msCoName](../includes/msconame-md.md)] Access 데이터베이스 또는 프로젝트에서 보고서를 가져올 수 있습니다. 단, 보고서 디자이너가 설치되어 있는 컴퓨터에 Access 2002 이상이 설치되어 있어야 합니다.  
  
 가져오기 기능을 사용하면 데이터베이스나 프로젝트 파일의 모든 보고서를 가져옵니다. Access 파일에 보고서가 많이 있을 경우 보고서를 가져올 개별 보고서 프로젝트를 만든 후 주 보고서 프로젝트에서 각 RDL 파일을 열 수 있습니다. 보고서를 보고서 디자이너로 가져와야 편집할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 일부 Access 보고서 개체는 지원되지 않습니다. 변환 되지 않은 항목은 **작업 목록** 창에 표시 됩니다. 자세한 내용은 [SSRS&#41;&#40;지원 되는 액세스 보고서 기능 ](../../2014/reporting-services/supported-access-report-features-ssrs.md)을 참조 하세요.  
  
### <a name="to-import-reports-from-microsoft-access"></a>Microsoft Access에서 보고서를 가져오려면  
  
1.  보고서를 가져올 프로젝트를 열거나 만듭니다.  
  
2.  **프로젝트** 메뉴에서 **보고서 가져오기**를 가리킨 다음 **Microsoft Access**를 클릭 합니다. 또는 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **보고서 가져오기**를 가리킨 다음 **Microsoft Access**를 클릭 합니다.  
  
3.  **열기** 대화 상자에서 보고서가 포함 된 Access 데이터베이스 (.mdb, .accdb) 또는 프로젝트 (.adp)를 선택한 다음 **열기**를 클릭 합니다. 그러면 데이터베이스 또는 프로젝트 파일의 모든 보고서가 가져와지고 솔루션 탐색기의 보고서 폴더에 나열됩니다.  
  
4.  빌드 오류에 대 한 **작업 목록** 창을 확인 합니다. **작업 목록** 창을 보려면 **보기** 메뉴를 열고 **다른 창**을 가리킨 다음 **작업 목록**를 클릭 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 디자이너로 보고서 디자인&#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  
  
