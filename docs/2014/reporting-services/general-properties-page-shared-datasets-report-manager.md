---
title: 일반 속성 페이지, 공유 데이터 집합 (보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 10798e41-24c3-4e69-893b-7ee6af7fc958
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bf433f27a5d8dc7f5e0efcf6f5774ed292d1e1a1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109072"
---
# <a name="general-properties-page-shared-datasets-report-manager"></a>일반 속성 페이지, 공유 데이터 세트(보고서 관리자)
  공유 데이터 세트 페이지를 사용하여 공유 데이터 세트 항목의 속성을 보고 관리할 수 있습니다.  
  
 보고서 관리자에서는 쿼리를 비롯한 공유 데이터 세트 정의를 보거나 변경할 수 없습니다. 정의를 변경하려면 제작 도구를 사용하여 정의를 열고 수정한 다음 보고서 서버에 저장합니다.  
  
 공유 데이터 세트를 사용하면 데이터 세트의 설정을, 해당 설정을 사용하는 보고서, 구성 요소 및 기타 카탈로그 항목과 별도로 관리할 수 있습니다.  
  
## <a name="navigation"></a>탐색  
 사용자 인터페이스(UI)에서 이 위치를 탐색하려면 다음 절차를 사용하십시오.  
  
###### <a name="to-open-the-shared-dataset-properties-page-for-a-shared-dataset"></a>공유 데이터 세트의 공유 데이터 세트 속성 페이지를 열려면  
  
1.  보고서 관리자를 열고 속성을 구성할 공유 데이터 세트를 찾습니다.  
  
2.  공유 데이터 세트 위로 마우스를 이동하고 드롭다운 화살표를 클릭합니다.  
  
3.  드롭다운 목록에서 **관리**를 클릭합니다. 일반 속성 페이지가 열립니다.  
  
## <a name="options"></a>변수  
 **이름**  
 보고서 서버 폴더 계층 구조에서 항목을 식별하는 데 사용되는 공유 데이터 세트의 이름을 입력합니다.  
  
 **설명**  
 공유 데이터 세트에 대한 정보를 제공합니다. 이 설명은 내용 페이지에 표시됩니다.  
  
 **목록 뷰에서 숨기기**  
 보고서 관리자에서 목록 뷰 모드를 사용하는 사용자가 볼 수 없게 공유 데이터 세트를 숨깁니다. 목록 뷰 모드는 보고서 서버 폴더 계층을 검색할 때 표시되는 기본 뷰 형식입니다. 목록 뷰에서 항목 이름과 설명은 페이지에 가로로 표시됩니다. 이 외에도 자세히 보기를 사용할 수 있습니다. 자세히 보기는 설명을 표시하지 않지만 항목에 대한 다른 정보는 포함합니다. 목록 뷰에서는 항목을 숨길 수 있지만 자세히 보기에서는 항목을 숨길 수 없습니다. 항목에 대한 액세스를 제한하려면 역할 할당을 만들어야 합니다.  
  
 **쿼리 실행 제한 시간**  
 쿼리 제한 시간이 초과되기까지의 시간(초)을 입력합니다. 0을 입력하면 쿼리 시간이 제한되지 않습니다.  
  
 **적용**  
 변경 내용을 저장합니다.  
  
 **Delete**  
 보고서 서버 데이터베이스에서 공유 데이터 세트를 제거합니다. 공유 데이터 세트를 삭제하면 보고서 또는 캐시된 버전이 비활성화됩니다. 보고서를 다시 활성화하려면 보고서 제작 도구에서 해당 보고서를 열고 동일한 이름과 동일한 필드 컬렉션을 갖는 데이터 세트를 지정합니다. 또는 동일한 필드 컬렉션을 갖는 다른 데이터 세트를 사용하도록 각 데이터 영역 참조를 업데이트할 수도 있습니다.  
  
 **이동**  
 보고서 서버 폴더 계층 구조 내의 다른 위치로 공유 데이터 세트를 옮깁니다. 이 단추를 클릭하면 폴더를 검색하여 새 폴더 위치를 찾을 수 있는 항목 이동 페이지가 열립니다. 자세한 내용은 [항목 이동 페이지 &#40;보고서 관리자&#41;](../../2014/reporting-services/move-items-page-report-manager.md)합니다.  
  
 **다운로드**  
 공유 데이터 세트 정의의 복사본을 추출합니다. 컴퓨터에 정의된 파일 연결에 따라 파일이 Visual Studio 또는 다른 애플리케이션에서 열립니다. 대부분의 경우 공유 데이터 세트는 XML 파일로 열립니다.  
  
 **바꾸기**  
 파일 시스템에 있는 .rsd 파일의 다른 정의로 공유 데이터 세트 정의를 바꿉니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 관리자&#40;SSRS 기본 모드&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [내용 페이지&#40;보고서 관리자&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [보고서 관리자 F1 도움말](../../2014/reporting-services/report-manager-f1-help.md)   
 [캐시 새로 고침 옵션 &#40;보고서 관리자&#41;](../../2014/reporting-services/cache-refresh-options-report-manager.md)   
 [캐싱 페이지, 공유 데이터 집합 &#40;보고서 관리자&#41;](../../2014/reporting-services/caching-page-shared-datasets-report-manager.md)   
 [공유 데이터 세트 관리](report-data/manage-shared-datasets.md)   
 [공유 데이터 세트 캐시&#40;SSRS&#41;](report-server/cache-shared-datasets-ssrs.md)  
  
  
