---
title: 플랫 파일 대상 구성(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.configureflatfiledest.f1
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8c596f37cb0a83682c5c8dff370a92a5d3d73eb5
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71285792"
---
# <a name="configure-flat-file-destination-sql-server-import-and-export-wizard"></a>플랫 파일 대상 구성(SQL Server 가져오기 및 내보내기 마법사)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  플랫 파일 대상을 선택한 경우 테이블을 복사하도록 지정하거나 쿼리를 지정한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사에서 **플랫 파일 대상 구성**을 표시합니다. 이 페이지에서 대상 플랫 파일에 대한 서식 옵션을 지정합니다. 필요에 따라 개별 열의 매핑을 검토하고 샘플 데이터를 미리 봅니다.  
  
## <a name="screen-shot-of-the-configure-flat-file-destination-page"></a>플랫 파일 대상 구성 페이지의 스크린샷  
 다음 스크린샷은 마법사의 **플랫 파일 대상 구성** 페이지 예를 보여 줍니다.
 
 이 예에서는 사용자가 일반적인 CSV(쉼표로 구분된 값) 파일을 만드는 다음 옵션을 지정했습니다.
-   **행 구분 기호**을 참조하세요. 출력의 각 데이터 행은 캐리지 리턴-줄 바꿈 조합으로 끝납니다.
-   **열 구분 기호**을 참조하세요. 각 행 내의 데이터 열은 쉼표로 구분됩니다.

 ![가져오기 및 내보내기 마법사의 플랫 파일 구성 페이지](../../integration-services/import-export-data/media/flat-file.png)
  
## <a name="pick-a-source-table"></a>원본 테이블 선택
 **원본 테이블 또는 뷰**  
-   이전 페이지에서 테이블을 복사하기로 지정한 경우 원본 드롭다운 목록에서 원본 테이블 또는 보기를 선택합니다.
-   쿼리를 제공한 경우 `"Query"`가 선택되고 유일한 옵션으로 표시됩니다.  

## <a name="specify-row-and-column-delimiters-for-the-output"></a>출력에 대한 행 및 열 구분 기호를 지정합니다.
 **행 구분 기호**  
 출력의 행을 구분할 구분 기호를 목록에서 선택합니다. *사용자 지정* 행 구분 기호를 지정할 수 있는 옵션은 없습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|행을 캐리지 리턴-줄 바꿈 조합으로 구분합니다.|  
|**{CR}**|행을 캐리지 리턴으로 구분합니다.|  
|**{LF}**|행을 줄 바꿈으로 구분합니다.|  
|**세미콜론 {;}**|행을 세미콜론으로 구분합니다.|  
|**콜론 {:}**|행을 콜론으로 구분합니다.|  
|**쉼표 {,}**|행을 쉼표로 구분합니다.|  
|**탭 {t}**|행을 탭으로 구분합니다.|  
|**세로 막대{&#124;}**|행을 세로 막대로 구분합니다.|  
  
 **열 구분 기호**  
 출력의 열을 구분할 구분 기호를 목록에서 선택합니다. *사용자 지정* 열 구분 기호를 지정할 수 있는 옵션은 없습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|열을 캐리지 리턴-줄 바꿈 조합으로 구분합니다.|  
|**{CR}**|열을 캐리지 리턴으로 구분합니다.|  
|**{LF}**|열을 줄 바꿈으로 구분합니다.|  
|**세미콜론 {;}**|열을 세미콜론으로 구분합니다.|  
|**콜론 {:}**|열을 콜론으로 구분합니다.|  
|**쉼표 {,}**|열을 쉼표로 구분합니다.|  
|**탭 {t}**|열을 탭으로 구분합니다.|  
|**세로 막대{&#124;}**|열을 세로 막대로 구분합니다.|  

## <a name="optionally-review-column-mappings-and-preview-data"></a>필요에 따라 열 매핑 검토 및 데이터 미리 보기

**매핑 편집**   
필요에 따라 **매핑 편집**을 클릭하여 선택한 테이블에 대한 **열 매핑** 대화 상자를 표시합니다. **열 매핑** 대화 상자를 사용하여 다음을 수행할 수 있습니다.
-   원본과 대상 간의 개별 열 매핑을 검토합니다.
-   복사하지 않을 열에 **무시** 를 선택하여 일부 열만 복사합니다.

자세한 내용은 [열 매핑](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)을 참조하세요.  

**미리 보기**  
필요에 따라 **미리 보기**를 클릭하여 **데이터 미리 보기** 대화 상자에서 최대 200개의 샘플 데이터 행을 미리 봅니다. 이를 통해 원하는 데이터를 마법사가 복사하는지 확인할 수 있습니다. 자세한 내용은 [데이터 미리 보기](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)를 참조하세요.  
  
데이터를 미리 본 후 마법사의 이전 페이지에서 선택한 옵션을 변경할 수도 있습니다. 이렇게 변경하려면 **플랫 파일 대상 구성** 페이지로 돌아간 다음 **뒤로** 를 클릭하여 선택 내용을 변경할 수 있는 이전 페이지로 돌아갑니다.  

## <a name="whats-next"></a>다음 단계  
 대상 플랫 파일에 대한 서식 옵션을 지정한 후 다음 페이지는 **패키지 저장 및 실행**입니다. 이 페이지에서는 작업을 즉시 실행할지 여부를 지정합니다. 구성에 따라 설정을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지로 저장하여 나중에 사용자 지정하고 다시 사용할 수도 있습니다. 자세한 내용은 [패키지 저장 및 실행](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)을 참조하세요.  

