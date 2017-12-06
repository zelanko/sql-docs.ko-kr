---
title: "파일 또는 보고서 업로드(보고서 관리자) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- publishing reports [Reporting Services], uploading files
- reports [Reporting Services], publishing
- uploading reports [Reporting Services]
- uploading files [Reporting Services]
- files [Reporting Services], uploading
ms.assetid: 79027e11-f4ba-4bfd-bd8c-d334e3da02a1
caps.latest.revision: "42"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: c5934844dd9570ab95ab5641d66a465f57725e55
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="upload-a-file-or-report-report-manager"></a>파일 또는 보고서 업로드(보고서 관리자)
  보고서 관리자에서는 업로드 기능을 제공하므로 클라이언트 응용 프로그램에서 보고서, 모델 및 기타 파일을 게시하지 않고도 이러한 항목을 보고서 서버에 추가할 수 있습니다. 파일 시스템에서 업로드한 파일은 보고서 서버에 항목으로 저장됩니다. 업로드한 파일 형식은 저장되는 방식에 따라 결정됩니다.  
  
-   .rdl 파일은 보고서로 저장됩니다.  
  
-   .smdl 파일은 보고서 모델로 저장됩니다.  
  
-   공유 데이터 원본 파일(.rds)을 비롯한 다른 모든 파일은 리소스로 업로드됩니다. 리소스는 보고서 서버에서 처리되지 않지만 보고서 서버가 MIME 형식의 파일을 지원하는 경우 보고서 관리자에서 볼 수 있습니다.  
  
### <a name="to-upload-a-file-or-report"></a>파일 또는 보고서를 업로드하려면  
  
1.  [보고서 관리자&#40;SSRS 기본 모드&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)를 시작합니다.  
  
2.  보고서 관리자에서 **내용** 페이지로 이동합니다. 항목을 추가할 폴더로 이동합니다.  
  
3.  **파일 업로드**를 클릭합니다.  
  
4.  **찾아보기** 를 클릭하여 업로드할 파일을 선택합니다. 보고서 정의 파일, 이미지, 문서 등 보고서 서버에서 사용할 수 있는 모든 파일을 업로드할 수 있습니다.  
  
5.  새 항목의 이름을 입력합니다. 항목 이름에 공백을 사용할 수 있지만 다음과 같은 예약 문자는 사용할 수 없습니다. ; ? : @ & = + , $ / * < > |.  
  
6.  기존 항목을 새 항목으로 바꾸려면 **항목이 있으면 덮어쓰기**를 선택합니다.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목:  
 [공유 데이터 원본 만들기, 삭제 또는 수정&#40;보고서 관리자&#41;](http://msdn.microsoft.com/library/cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2)   
 [내용 페이지&#40;보고서 관리자&#41;](http://msdn.microsoft.com/library/6b16869b-158a-4934-9c85-bee934b35378)   
 [파일 업로드 페이지&#40;보고서 관리자&#41;](http://msdn.microsoft.com/library/7bb3166f-9374-4449-b66a-ffb77298507d)   
 [폴더에 파일 업로드](../../reporting-services/report-server/upload-files-to-a-folder.md)  
  
  
