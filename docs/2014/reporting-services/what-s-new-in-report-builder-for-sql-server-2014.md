---
title: SQL Server 2014에 대 한 보고서 작성기의 새로운 기능&#39;Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 8223c19b-4b0d-4b1d-a042-9a726c18e708
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 35ac6191407e02a2dc15ab210c5e9276e761df75
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66098678"
---
# <a name="what39s-new-in-report-builder-for-sql-server-2014"></a>SQL Server 2014에 대 한 보고서 작성기의 새로운 기능&#39;
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]에는 많은 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기능이 도입되었습니다.  
  
 다른 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 제품 및 기술에 대 한이 릴리스의 기능에 대 한 자세한 내용은 [SQL Server 2014의 새로운](../sql-server/what-s-new-in-sql-server-2016.md)기능을 참조 하세요.  
  
> [!TIP]  
>  이 릴리스의 새로운 기능에 대 한 최신 정보 및 리소스는 [SQL Server Reporting Services (SSRS)의 새로운 기능에 대 한 추가 정보](https://go.microsoft.com/fwlink/?LinkId=207147)를 참조 하세요.  
  
##  <a name="excel-renderer-for-microsoft-excel-2007-2010-and-microsoft-excel-2003"></a><a name="ExcelRenderer"></a>Microsoft Excel 2007-2010 및 Microsoft Excel 2003 용 excel 렌더러  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]의 새로운 기능인 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Excel 렌더링 확장 프로그램은 Word, Excel 및 PowerPoint용 Microsoft Office 호환 기능 팩이 설치된 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 2003뿐만 아니라 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 2007-2010과도 호환되는 Excel 문서로 보고서를 렌더링합니다 형식은 Office Open XML이고 파일 확장명은 .xlsx입니다.  
  
 이 Excel 렌더링 확장 프로그램은 Excel 2003과 호환되는 이전 버전의 제한 사항을 제거합니다. 다음은 렌더링 확장 프로그램에서 향상된 내용을 나열합니다.  
  
-   워크시트당 최대 행 수는 1,048,576입니다.  
  
-   워크시트당 최대 열 수는 16,384입니다.  
  
-   워크시트에서 허용되는 색상 수는 약 1600만개(24비트 색)입니다.  
  
-   ZIP 압축을 통해 파일 크기를 줄일 수 있습니다.  
  
 자세한 내용은 [Microsoft Excel로 내보내기&#40;보고서 작성기 및 SSRS&#41;](report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)에서 이 데이터로 작업할 수 있습니다.  
  
##  <a name="word-renderer-for-microsoft-word-2007-2010-and-microsoft-word-2003"></a><a name="WordRenderer"></a>Microsoft Word 2007-2010 및 Microsoft Word 2003 용 word 렌더러  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]의 새로운 기능인 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Word 렌더링 확장 프로그램은 Word, Excel 및 PowerPoint용 [!INCLUDE[ofprword](../includes/ofprword-md.md)] Office 호환 기능 팩이 설치된 [!INCLUDE[ofprword](../includes/ofprword-md.md)] 2003뿐만 아니라 [!INCLUDE[msCoName](../includes/msconame-md.md)] 2007-2010과도 호환되는 Word 문서로 보고서를 렌더링합니다. 형식은 Office Open XML이고 파일 확장명은 docx입니다.  
  
 Word 2007-2010의 새로운 기능을 내보낸 보고서에서 사용할 수 있을 뿐만 아니라 보고서를 *.docx 파일로 내보낼 경우 크기를 줄일 수 있습니다. Word 렌더러를 사용하여 내보낸 보고서는 일반적으로 동일한 보고서를 Word 2003 렌더러를 사용하여 내보낼 때보다 매우 작습니다.  
  
 자세한 내용은 [Microsoft Word로 내보내기&#40;보고서 작성기 및 SSRS&#41;](report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md)에서 이 데이터로 작업할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2014의 보고서 작성기](report-builder/report-builder-in-sql-server-2016.md)  
  
  
