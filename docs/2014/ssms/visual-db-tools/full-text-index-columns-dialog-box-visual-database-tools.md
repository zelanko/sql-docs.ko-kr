---
title: 전체 텍스트 인덱스 열 대화 상자(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.fulltextcolumn
ms.assetid: a6f41c5c-d950-4d64-9e42-d062925917b6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8ece0e6856f43e2296fb0feab4abe38ffbba568b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63028330"
---
# <a name="full-text-index-columns-dialog-box-visual-database-tools"></a>전체 텍스트 인덱스 열 대화 상자(Visual Database Tools)
  이 대화 상자에는 테이블 디자이너에 열려 있는 테이블에 대한 전체 텍스트 인덱스와 관련된 열이 나열됩니다. 이 대화 상자를 열려면 테이블 디자이너에서 테이블을 마우스 오른쪽 단추로 클릭하고 **전체 텍스트 인덱스**를 선택한 다음, **전체 텍스트 인덱스** 대화 상자에서 보거나 편집하려는 열이 포함된 인덱스를 클릭하고 오른쪽 표에서 **열** 필드를 클릭한 후 줄임표( **...** )를 클릭합니다.  
  
## <a name="options"></a>변수  
 **열**  
 전체 텍스트 인덱스에 관련된 열의 이름을 표시합니다. 열을 추가하려면 비어 있는 첫 번째 셀을 클릭하고 드롭다운 목록에서 열을 선택합니다. 텍스트를 기반으로 한 열이나 이미지 데이터 형식의 열만 선택할 수 있습니다.  
  
 **데이터 형식**  
 각 열의 데이터 형식을 표시합니다. 읽기 전용 속성입니다. 데이터 형식을 변경하려면 테이블 디자이너에서 테이블을 열고 열을 클릭한 다음 **열 속성** 탭에서 데이터 형식을 편집합니다.  
  
 **열로 형식화**  
 이 옵션은 데이터 형식이 `image`인 열에만 적용됩니다. 이 옵션에서 제공하는 드롭다운 목록을 사용하여 다른 열을 선택하면 선택한 열에서 현재 열의 데이터 형식을 나타내도록 만들 수 있습니다. 현재 열의 데이터 형식이 `image`가 아닌 경우 값은 없음이 됩니다.  
  
 데이터 형식이 `image`인 열에는 Microsoft Office 파일(.doc, .xls 및 .ppt 파일), 텍스트 파일(.txt 파일), HTML 파일(.htm 파일)이 포함될 수 있고, 이 열의 데이터 형식을 이미지로 설정하면 전체 텍스트 검색을 통해 파일 내용을 검색할 수 있습니다.  
  
 **언어**  
 사용할 수 있는 언어를 나열합니다. 열 데이터에 해당하는 언어를 드롭다운 목록에서 선택합니다. 예를 들어 사용 중인 운영 체제는 영어이지만 독일어 텍스트가 포함된 열을 인덱싱하려는 경우 드롭다운 목록에서 독일어를 선택하면 인덱싱 속도를 향상시킬 수 있습니다.  
  
 **통계 의미 체계**  
 선택한 열에 대해 의미 체계 인덱싱을 사용하도록 설정할지 여부를 선택합니다. 자세한 내용은 [의미 체계 검색&#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md)을 참조하세요.  
  
 **통계 의미 체계** 를 선택하기 전에 **언어**를 선택했으며 선택한 언어에 연결된 의미 체계 언어 모델이 없으면 **통계 의미 체계** 확인란은 사용할 수 없습니다. **언어** 를 선택하기 전에 **통계 의미 체계**를 선택한 경우 드롭다운 콤보 상자에서 사용할 수 있는 언어가 의미 체계 언어 모델에서 지원하는 언어로 제한됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [전체 텍스트 인덱스 대화 상자&#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
  
