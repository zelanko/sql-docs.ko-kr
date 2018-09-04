---
title: 보고서 서버에서 파일 또는 보고서 업로드 | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reports
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- publishing reports [Reporting Services], uploading files
- reports [Reporting Services], publishing
- uploading reports [Reporting Services]
- uploading files [Reporting Services]
- files [Reporting Services], uploading
ms.assetid: 79027e11-f4ba-4bfd-bd8c-d334e3da02a1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b24b1d8a73aa2f371642f9b8a54b20471e20cb23
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43277292"
---
# <a name="upload-a-file-or-report-in-the-report-server"></a>보고서 서버에서 파일 또는 보고서 업로드
보고서 서버의 웹 포털에서는 업로드 기능을 제공하므로 클라이언트 응용 프로그램에서 보고서 및 기타 파일을 게시하지 않고도 이러한 항목을 보고서 서버에 추가할 수 있습니다. 파일 시스템에서 업로드한 파일은 보고서 서버에 항목으로 저장됩니다. 업로드한 파일 형식은 저장되는 방식에 따라 결정됩니다.  
  
-   .rdl 파일은 페이지를 매긴 보고서로 저장됩니다.  
  
-   공유 데이터 원본 파일(.rds)을 비롯한 다른 모든 파일은 리소스로 업로드됩니다. 리소스는 보고서 서버에서 처리되지 않지만 보고서 서버가 MIME 형식의 파일을 지원하는 경우 웹 포털에서 볼 수 있습니다.  
  
### <a name="to-upload-a-file-or-report"></a>파일 또는 보고서를 업로드하려면  
  
1.  웹 포털에서 **업로드**를 클릭합니다.  
  
4.  업로드할 파일을 찾습니다. 보고서 정의 파일, 이미지, 문서 등 보고서 서버에서 사용할 수 있는 모든 파일을 업로드할 수 있습니다.  
  
5.  새 항목의 이름을 입력합니다. 항목 이름에 공백을 사용할 수 있지만 다음과 같은 예약 문자는 사용할 수 없습니다. ; ? : \@ & = + , $ / * < > |.  
  
6.  기존 항목을 새 항목으로 바꾸려면 **항목이 있으면 덮어쓰기**를 선택합니다.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>참고 항목   
[공유 데이터 원본 만들기, 수정 및 삭제](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)
[폴더에 파일 업로드](../../reporting-services/report-server/upload-files-to-a-folder.md)  
  
  
