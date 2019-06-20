---
title: 파일 또는 보고서 업로드(보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- publishing reports [Reporting Services], uploading files
- reports [Reporting Services], publishing
- uploading reports [Reporting Services]
- uploading files [Reporting Services]
- files [Reporting Services], uploading
ms.assetid: 79027e11-f4ba-4bfd-bd8c-d334e3da02a1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 56a9c380b8cc88202cdcb4c4dca54aab2d1fa4a6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102401"
---
# <a name="upload-a-file-or-report-report-manager"></a>파일 또는 보고서 업로드(보고서 관리자)
  보고서 관리자에서는 업로드 기능을 제공하므로 클라이언트 애플리케이션에서 보고서, 모델 및 기타 파일을 게시하지 않고도 이러한 항목을 보고서 서버에 추가할 수 있습니다. 파일 시스템에서 업로드한 파일은 보고서 서버에 항목으로 저장됩니다. 업로드한 파일 형식은 저장되는 방식에 따라 결정됩니다.  
  
-   .rdl 파일은 보고서로 저장됩니다.  
  
-   .smdl 파일은 보고서 모델로 저장됩니다.  
  
-   공유 데이터 원본 파일(.rds)을 비롯한 다른 모든 파일은 리소스로 업로드됩니다. 리소스는 보고서 서버에서 처리되지 않지만 보고서 서버가 MIME 형식의 파일을 지원하는 경우 보고서 관리자에서 볼 수 있습니다.  
  
### <a name="to-upload-a-file-or-report"></a>파일 또는 보고서를 업로드하려면  
  
1.  [보고서 관리자&#40;SSRS 기본 모드&#41;](../report-manager-ssrs-native-mode.md)를 시작합니다.  
  
2.  보고서 관리자에서 **내용** 페이지로 이동합니다. 항목을 추가할 폴더로 이동합니다.  
  
3.  **파일 업로드**를 클릭합니다.  
  
4.  **찾아보기** 를 클릭하여 업로드할 파일을 선택합니다. 보고서 정의 파일, 이미지, 문서 등 보고서 서버에서 사용할 수 있는 모든 파일을 업로드할 수 있습니다.  
  
5.  새 항목의 이름을 입력합니다. 항목 이름에 공백을 사용할 수 있지만 다음과 같은 예약 문자는 사용할 수 없습니다. ; ? : \@ & = + , $ / * \< > |.  
  
6.  기존 항목을 새 항목으로 바꾸려면 **항목이 있으면 덮어쓰기**를 선택합니다.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [공유 데이터 원본 만들기, 삭제 또는 수정&#40;보고서 관리자&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [내용 페이지&#40;보고서 관리자&#41;](../contents-page-report-manager.md)   
 [파일 업로드 페이지&#40;보고서 관리자&#41;](../upload-file-page-report-manager.md)   
 [폴더에 파일 업로드](../report-server/upload-files-to-a-folder.md)  
  
  
