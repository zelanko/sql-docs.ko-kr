---
title: 일반 속성 페이지, 보고서 파트 (보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 93ddce72-31f1-42f7-abd5-8191acbb00c5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: aa3f8b6ec0cd81f1a29ea3262bd3ec52dd8158ae
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66109094"
---
# <a name="general-properties-page-report-parts-report-manager"></a>일반 속성 페이지, 보고서 파트(보고서 관리자)
  속성 페이지를 사용하여 보고서 파트의 일반 속성을 보고 수정할 수 있습니다.  
  
 보고서 관리자에서는 보고서 파트의 모양 및 기능을 보거나 변경할 수 없습니다. 디자인을 변경하려면 제작 도구를 사용하여 디자인을 열고 수정한 후 다시 서버에 게시해야 합니다.  
  
## <a name="navigation"></a>탐색  
 사용자 인터페이스(UI)에서 이 위치를 탐색하려면 다음 절차를 사용하십시오.  
  
###### <a name="to-open-the-properties-page-for-a-report-part"></a>보고서 파트의 속성 페이지를 열려면  
  
1.  보고서 관리자를 열고 보고서 속성을 구성할 보고서 파트를 찾습니다.  
  
2.  보고서 파트 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
3.  드롭다운 목록에서 **관리**를 클릭합니다. 일반 속성 페이지가 열립니다.  
  
## <a name="options"></a>변수  
 **수정한 날짜**  
 서버에서 보고서 파트 속성이 마지막으로 수정되거나 새 버전의 보고서 파트가 서버에 게시된 날짜 및 시간입니다. 읽기 전용입니다.  
  
 **에 의해 수정**  
 보고서 파트를 마지막으로 수정한 사람의 이름입니다. 읽기 전용입니다.  
  
 **만든 날짜**  
 보고서 파트가 서버에 처음 게시된 날짜 및 시간입니다. 읽기 전용입니다.  
  
 **만든**  
 보고서 파트를 처음에 만든 사람의 이름입니다. 읽기 전용입니다.  
  
 **크기**  
 보고서 파트의 파일 크기입니다. 읽기 전용입니다.  
  
 **이름**  
 보고서 파트를 식별하는 이름을 입력합니다.  
  
 **설명**  
 보고서 파트에 대한 정보를 제공합니다. 설명은 보고서 관리자의 내용 페이지에 나타납니다. 사용자가 보고서 제작 도구에서 보고서 파트를 검색할 때 설명 텍스트를 검색할 수 있습니다.  
  
 **목록 뷰에서 숨기기**  
 보고서 관리자에서 목록 뷰 모드를 사용하는 사용자가 볼 수 없게 보고서 파트를 숨기려면 선택합니다. 목록 뷰 모드는 보고서 서버 폴더 계층을 찾아 볼 때 표시되는 기본 뷰 형식입니다. 목록 뷰에서는 항목을 숨길 수 있지만 자세히 보기에서는 항목을 숨길 수 없습니다. 항목에 대한 액세스를 제한하려면 역할 할당을 만들어야 합니다.  
  
 **형식**  
 보고서 파트의 유형입니다. 읽기 전용입니다.  
  
 **적용**  
 변경 내용을 저장합니다.  
  
 **Delete**  
 보고서 서버 데이터베이스에서 보고서 파트를 제거합니다. 서버에서 보고서 파트를 삭제해도 보고서 파트가 추가된 기존 보고서는 렌더링됩니다.  
  
 **이동**  
 보고서 서버 폴더 계층 구조 내에서 보고서 파트를 이동하기 위해 항목 이동 페이지를 열려면 클릭합니다. 자세한 내용은 [항목 이동 페이지 &#40;보고서 관리자&#41;](../../2014/reporting-services/move-items-page-report-manager.md)합니다.  
  
 **다운로드**  
 .rsc 파일로 저장할 보고서 파트 정의의 복사본을 추출합니다. .rsc 파일을 보고서 서버 폴더에 업로드하거나 보고서 서버 폴더의 기존 보고서 파트를 바꾸는 데 사용할 수 있습니다.  
  
 **바꾸기**  
 보고서 파트 정의를 .rsc 파일의 다른 정의로 바꿉니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 파트 관리](report-design/managing-report-parts.md)   
 [보고서 관리자&#40;SSRS 기본 모드&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [내용 페이지&#40;보고서 관리자&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [보고서 파트&#40;보고서 작성기 및 SSRS&#41;](report-parts-report-builder-and-ssrs.md)   
 [보고서 관리자 F1 도움말](../../2014/reporting-services/report-manager-f1-help.md)   
 [보고서 작성기의 보고서 파트 및 데이터 집합](report-data/report-parts-and-datasets-in-report-builder.md)  
  
  
