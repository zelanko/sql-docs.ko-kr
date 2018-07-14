---
title: 플랫 파일 (SSAS)에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connflatfile.f1
ms.assetid: a365991e-eded-4cd8-89c0-0daf6d658d15
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 19f315644a829f543a88bdb135dcf25d4d8b5b15
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37201983"
---
# <a name="connect-to-a-flat-file-ssas"></a>플랫 파일에 연결(SSAS)
  **테이블 가져오기 마법사**의 이 페이지를 사용하면 플랫 파일(.txt), 탭으로 구분된 파일(.tab) 또는 쉼표로 구분된 파일(.csv)에 연결할 수 있습니다. [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 마법사에 액세스하려면 **모델** 메뉴에서 **데이터 원본에서 가져오기**를 클릭합니다.  
  
 플랫 파일에 연결하려면 컴퓨터에 적절한 ACE 공급자를 설치해야 합니다. 자세한 내용은 [지원되는 데이터 원본&#40;SSAS 테이블 형식&#41;](tabular-models/data-sources-supported-ssas-tabular.md)을 참조하세요.  
  
> [!NOTE]  
>  이 페이지에서 파일을 선택하는 경우 현재 사용자의 자격 증명이 사용됩니다. 하지만 가장 정보 페이지에 지정된 사용자에게 선택한 파일을 읽을 수 있는 권한이 없는 경우에는 가져오기 작업이 실패합니다.  
  
## <a name="uielement-list"></a>UIElement 목록  
 **연결 이름**  
 이 데이터 원본 연결의 고유 이름을 입력합니다. 이 이름은 반드시 입력해야 합니다.  
  
 **파일 경로**  
 파일의 전체 경로를 지정합니다.  
  
 **찾아보기**  
 파일을 사용할 수 있는 위치로 이동합니다.  
  
 **열 구분 기호**  
 사용 가능한 열 구분 기호의 목록에서 선택합니다. 텍스트에 거의 사용되지 않는 구분 기호를 선택합니다.  
  
|값|Description|  
|-----------|-----------------|  
|탭(t)|열이 탭(t)으로 구분됩니다.|  
|쉼표(,)|열이 쉼표(,)로 구분됩니다.|  
|세미콜론(;)|열이 세미콜론(;)으로 구분됩니다.|  
|공백( )|열이 공백( )으로 구분됩니다.|  
|콜론(:)|열이 콜론(:)으로 구분됩니다.|  
|세로 막대(&#124;)|열이 세로 막대(&#124;)로 구분됩니다.|  
  
 **고급**  
 플랫 파일에 대한 인코딩 및 로캘 옵션을 지정합니다.  
  
 **첫 번째 행을 열 머리글로 사용**  
 첫 번째 데이터 행을 대상 테이블의 열 머리글로 사용할지 여부를 지정합니다.  
  
 **데이터 미리 보기**  
 선택한 파일의 데이터를 미리 보고 다음 옵션을 사용하여 데이터 가져오기를 수정합니다.  
  
> [!NOTE]  
>  파일의 첫 50행만 이 미리 보기에 표시됩니다.  
  
|옵션|Description|  
|------------|-----------------|  
|**열 머리글의 확인란**|데이터 가져오기에 열을 포함하려면 이 확인란을 선택하고, 데이터 가져오기에서 열을 제거하려면 이 확인란의 선택을 취소합니다.|  
|**열 머리글의 아래쪽 화살표 단추**|열의 데이터를 정렬하고 필터링합니다.|  
  
 **행 필터 지우기**  
 열의 데이터에 적용된 모든 필터를 제거합니다.  
  
  
