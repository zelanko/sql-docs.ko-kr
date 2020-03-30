---
title: 원시 파일 원본 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.rawfilesource.f1
- sql13.dts.designer.rawfilesourceconnectionmanager.f1
- sql13.dts.designer.rawfilesourcecolumns.f1
helpviewer_keywords:
- sources [Integration Services], Raw File
- raw data [Integration Services]
- Raw File source
ms.assetid: 5b4daea5-7f76-4674-aa77-0a79f9f97f7d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e35fffa75f72b4edaddba344d166cb1c89fb3338
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71298133"
---
# <a name="raw-file-source"></a>원시 파일 원본

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  원시 파일 원본은 파일에서 원시 데이터를 읽습니다. 원본의 기본 데이터 표현을 사용하므로 데이터를 변환하거나 거의 구문 분석할 필요도 없습니다. 따라서 원시 파일 원본은 플랫 파일 및 OLE DB 원본과 같은 다른 원본보다 빨리 데이터를 읽을 수 있습니다.  
  
 원시 파일 원본은 원시 파일 대상에서 이전에 기록한 원시 데이터를 검색하는 데 사용합니다. 또한 원시 파일 원본이 열만 포함된 빈 원시 파일(메타데이터 전용 파일)을 가리키도록 설정할 수 있습니다. 패키지를 실행할 필요없이 원시 파일 대상을 사용하여 메타데이터 전용 파일을 생성합니다. 자세한 내용은 [Raw File Destination](../../integration-services/data-flow/raw-file-destination.md)을 참조하세요.  
  
 원시 파일 서식에는 정렬 정보가 포함됩니다. 원시 파일 대상에는 문자열 열을 위한 비교 플래그를 포함하여 모든 정렬 정보가 저장됩니다. 원시 파일 원본은 정렬 정보를 읽고 적용합니다. 고급 편집기를 사용하면 파일의 정렬 플래그를 무시하도록 원시 파일 원본을 구성할 수 있습니다. 비교 플래그에 대한 자세한 내용은 [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md)를 참조하십시오.  
  
 원시 파일 원본에서 읽을 파일 이름을 지정하여 원시 파일을 구성합니다.  
  
> [!NOTE]  
>  이 원본은 연결 관리자를 사용하지 않습니다.  
  
 이 원본에는 하나의 출력이 있습니다. 오류 출력은 지원하지 않습니다.  
  
## <a name="configuration-of-the-raw-file-source"></a>원시 파일 원본 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [원시 파일 사용자 지정 속성](../../integration-services/data-flow/raw-file-custom-properties.md)  
  
## <a name="related-tasks"></a>관련 작업  
 구성 요소의 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="related-content"></a>관련 내용  
  
-   sqlservercentral.com의 블로그 항목 - [원시 파일의 놀라운 기능](https://www.sqlservercentral.com/blogs/stratesql/archive/2011/1/1/31-days-of-ssis-_1320_-raw-files-are-awesome-_2800_1_2F00_31_2900_.aspx)  
  
## <a name="raw-file-source-editor-connection-manager-page"></a>원시 파일 원본 편집기(연결 관리자 페이지)
  원시 파일 원본은 파일에서 원시 데이터를 읽습니다. 원본의 기본 데이터 표현을 사용하므로 데이터를 변환하거나 거의 구문 분석할 필요도 없습니다.   
## <a name="raw-file-source-editor-columns-page"></a>원시 파일 원본 편집기(열 페이지)
  원시 파일 원본은 파일에서 원시 데이터를 읽습니다. 원본의 기본 데이터 표현을 사용하므로 데이터를 변환하거나 거의 구문 분석할 필요도 없습니다.   
## <a name="see-also"></a>참고 항목  
 [Raw File Destination](../../integration-services/data-flow/raw-file-destination.md)   
 [데이터 흐름](../../integration-services/data-flow/data-flow.md)  
  
  
