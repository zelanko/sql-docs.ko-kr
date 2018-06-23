---
title: 폴더에 파일 업로드 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- publishing reports [Reporting Services], uploading files
- reports [Reporting Services], publishing
- uploading reports [Reporting Services]
- uploading files [Reporting Services]
- files [Reporting Services], uploading
- files [Reporting Services]
- folders [Reporting Services], uploading files to
ms.assetid: 2f99a288-d4aa-4c64-b310-e457a2aef2c5
caps.latest.revision: 41
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 579d4d16e72b349ac4c2aa5d083d8dc1cfeb85a1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088779"
---
# <a name="upload-files-to-a-folder"></a>폴더에 파일 업로드
  파일 시스템에서 파일을 업로드하여 보고서 서버 데이터베이스에 관리되는 항목으로 저장할 수 있습니다. 파일을 업로드할 때 발생하는 상황은 파일 형식에 따라 다릅니다.  
  
-   .rdl 파일을 업로드하는 것은 보고서를 게시하는 것과 같습니다.  
  
-   다른 파일을 업로드하면 보고서 서버 데이터베이스에 단일 이진 개체로 추가됩니다. 이 파일은 보고서 서버에 리소스로 게시됩니다. 리소스는 어떤 파일 형식이든 상관없습니다. 파일 확장명이 알려진 MIME 형식과 일치하면 해당 MIME 형식을 나타내는 아이콘이 리소스 형식을 식별하는 데 사용됩니다. 그 밖의 일반 파일 아이콘은 리소스를 나타냅니다.  
  
> [!NOTE]  
>  공유 데이터 원본을 만들 때는 보고서 데이터 원본 파일(.rds)을 업로드할 수 없습니다. .rds 파일은 보고서 디자이너에서만 사용됩니다. 이 파일은 보고서 관리자를 통해 정의하고 관리하는 공유 데이터 원본 항목에는 내용을 제공할 수 없습니다. 데이터 원본을 업로드하는 대신 .rds 파일을 기반으로 공유 데이터 원본을 만드는 스크립트를 작성할 수 있습니다.  
  
 업로드한 항목의 최대 파일 크기는 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]에 의해 결정됩니다. 기본적으로 최대 크기는 4MB입니다.  
  
 보고서 서버 데이터베이스에 업로드한 파일은 폴더 계층에 다음 아이콘으로 표시됩니다.  
  
 ![보고서 아이콘](../media/hlp-16doc.gif "보고서 아이콘")  
보고서 아이콘  
  
 ![모델 아이콘](../media/model-icon.gif "모델 아이콘")  
보고서 모델 아이콘  
  
 ![일반 리소스 아이콘](../media/hlp-16file.gif "일반 리소스 아이콘")  
일반 리소스 아이콘  
  
 파일을 업로드하는 경우 파일은 항상 현재 선택된 폴더에 놓입니다. 처음에 항목을 포함시킬 폴더로 이동하거나 파일을 업로드한 다음 나중에 최종 위치로 이동할 수 있습니다.  
  
 파일을 업로드하려면 보고서 관리자를 사용합니다. 보고서 서버로 파일을 업로드할 수 있는지 여부는 사용자의 역할 할당에 속하는 태스크에 따라 다릅니다. 기본 보안을 사용할 경우 로컬 관리자는 보고서 서버에 항목을 추가할 수 있습니다. 내 보고서를 설정한 경우 내 보고서 폴더를 갖고 있는 모든 사용자가 해당 폴더로 항목을 업로드할 수 있습니다. 사용자 지정 역할 할당을 사용하는 경우 역할 할당에 폴더 관리 지원 태스크가 포함되어야 합니다.  
  
|수행 작업|포함되는 태스크|  
|----------------|-------------------------|  
|폴더에 .rdl 파일 업로드|보고서 관리|  
|파일을 이진 개체로 업로드|리소스 관리|  
|폴더의 내용 보기|리소스 보기, 보고서 보기|  
  
## <a name="see-also"></a>관련 항목  
 [보고서 관리자 &#40;SSRS 기본 모드&#41;]... / 보고서-관리자-ssrs-네이티브-mode.md)   
 [기본 모드 보고서 서버에 대한 사용 권한 부여](../security/granting-permissions-on-a-native-mode-report-server.md)   
 [태스크 및 권한](../security/tasks-and-permissions.md)   
 [파일 또는 보고서 업로드&#40;보고서 관리자&#41;](../reports/upload-a-file-or-report-report-manager.md)  
  
  