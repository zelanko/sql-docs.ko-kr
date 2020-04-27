---
title: 내 보고서 사용(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 49c3c1da-b106-41f6-9173-16ff225bade8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 410cb4de6b89052493618404df3e595fd6999936
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66107574"
---
# <a name="using-my-reports-report-builder-and-ssrs"></a>내 보고서 사용(보고서 작성기 및 SSRS)
  기본 모드로 구성된 보고서 서버에서 내 보고서 폴더는 소유한 보고서를 저장하고 작업하는 데 사용할 수 있는 개인 작업 영역입니다. 다른 보고서 서버 폴더는 공용 폴더이며 일반적으로 사용자가 폴더 내용을 추가하거나 수정하려면 고급 사용 권한이 있어야 합니다. 이와는 달리 내 보고서 폴더는 사용자 관리 작업 영역입니다. 보고서와 폴더를 추가하거나 제거할 수 있으며 사용자 개인 설정을 사용하여 링크된 보고서를 저장할 수 있습니다.  
  
 개념적으로 내 보고서 폴더는 Windows 파일 시스템의 내 문서 폴더와 비슷합니다. 각 사용자가 내 보고서라는 폴더를 가지고 있더라도 액세스하는 폴더는 모두 다릅니다. 보고서 서버 관리자를 제외한 사용자는 다른 사용자가 소유한 내 보고서 폴더의 내용에 액세스할 수 없습니다.  
  
 내 보고서 기능은 선택적이며 보고서 서버 관리자가 설정을 해제할 수 있습니다. 이 기능을 설정하면 홈 폴더에 내 보고서 폴더가 나타나며 보고서 관리자나 웹 브라우저를 사용하여 이 폴더에 액세스할 수 있습니다. 자세한 내용은 [보고서 관리자에서 보고서 찾기 및 보기&#40;보고서 작성기 및 SSRS&#41;](finding-and-viewing-reports-in-the-web-portal-report-builder-and-ssrs.md)를 참조하세요.  
  
 SharePoint 통합 모드로 구성된 보고서 서버에는 내 보고서 폴더에 해당하는 폴더가 없습니다. 자세한 내용은 [보고서 찾기, 보기 및 관리&#40;보고서 작성기 및 SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="ways-to-use-my-reports"></a>내 보고서 사용 방법  
 사용자가 보고서, 폴더 및 기타 항목을 추가할 때까지는 내 보고서가 비어 있습니다. 내 보고서에 내용을 추가하는 방법은 다음과 같습니다.  
  
-   링크된 개인 보고서를 만들어 내 보고서에 저장합니다. 일부 보고서는 링크로 연결할 수 없습니다. 자세한 내용은 [연결된 보고서 만들기](../reports/create-a-linked-report.md)를 참조하세요.  
  
-   파일 시스템에서 보고서 정의 파일(.rdl), 보고서 모델 파일(.smdl) 또는 기타 파일을 업로드합니다. 모든 파일을 업로드할 수 있지만 보고서 서버에서는 파일 확장명이 .rdl 또는 .smdl인 보고서 파일만 처리합니다. 자세한 내용은 SQL Server 온라인 설명서의 [Reporting Services 설명서](https://go.microsoft.com/fwlink/?linkid=121312)에서 “보고서 정의” 및 [파일 또는 보고서 업로드&#40;보고서 관리자&#41;](../reports/upload-a-file-or-report-report-manager.md)를 참조하세요.  
  
-   사용자 보고서를 만들어 내 보고서에 게시합니다. 자세한 내용은 [보고서 디자인 뷰&#40;보고서 작성기&#41;](report-design-view-report-builder.md)를 참조하세요.  
  
 일반적으로 내 보고서에 대한 사용 권한으로 폴더를 직접 관리할 수 있습니다. 그러나 사용자가 수행할 수 있는 태스크는 보고서 서버 관리자가 결정합니다. 사용 권한이 부족하여 내 보고서에서 작업할 수 없는 경우 보고서 서버 관리자에게 문의하십시오.  
  
## <a name="searching-my-reports"></a>내 보고서 검색  
 보고서 서버 데이터베이스를 검색할 때 검색 범위에 해당 사용자의 내 보고서 폴더 내용만 포함되고 다른 사용자의 내 보고서 폴더 내용은 포함되지 않습니다. 검색 결과에는 사용자가 액세스할 수 있는 보고서만 나열됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 찾기, 보기 및 관리&#40;보고서 작성기 및 SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
