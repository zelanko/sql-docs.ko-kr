---
title: 데이터 미리 보기 대화 상자(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 02/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.previewdata.f1
ms.assetid: 423ac26a-ba02-4fdf-88b4-07995fe4a97e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e59c3aa71cbbff6f955c67d033713f7a27dfbb28
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86920184"
---
# <a name="preview-data-dialog-box-sql-server-import-and-export-wizard"></a>데이터 미리 보기 대화 상자(SQL Server 가져오기 및 내보내기 마법사)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  복사할 데이터를 지정한 후 필요에 따라 **미리 보기** 를 클릭하여 **데이터 미리 보기** 대화 상자를 열 수 있습니다. 이 페이지에서는 데이터 원본의 샘플 데이터 행을 최대 200개까지 미리 볼 수 있습니다. 이를 통해 원하는 데이터를 마법사가 복사하는지 확인할 수 있습니다.
  
## <a name="screen-shot-of-the-preview-data-page"></a>데이터 미리 보기 페이지의 스크린샷 
 다음 스크린샷은 마법사의 **데이터 미리 보기** 대화 상자를 보여 줍니다.  
 
![가져오기 및 내보내기 마법사의 데이터 미리 보기 페이지](../../integration-services/import-export-data/media/preview-data.png "가져오기 및 내보내기 마법사의 데이터 미리 보기 페이지")  
  
## <a name="preview-sample-data"></a>샘플 데이터 미리 보기  
 **원본**  
마법사가 데이터 원본에서 데이터를 로드하는 데 사용하는 쿼리를 표시합니다.

복사할 테이블을 선택한 경우 **원본** 필드는 테이블 이름 대신 `SELECT * FROM <table>` 쿼리를 표시합니다. 
  
 **샘플 데이터 표**  
 쿼리가 데이터 원본에서 반환하는 샘플 데이터의 행을 최대 200개까지 표시합니다.  


## <a name="thats-not-right-i-want-to-change-something"></a>잘못된 부분이 있습니다. 변경하고 싶습니다.
데이터를 미리 본 후 마법사의 이전 페이지에서 선택한 옵션을 변경할 수도 있습니다. 변경하려면 **확인**을 클릭하여 **원본 테이블 및 보기 선택** 페이지로 돌아간 다음 **뒤로**를 클릭하여 선택 내용을 변경할 수 있는 이전 페이지로 돌아갑니다.

## <a name="whats-next"></a>다음 단계  
 복사할 데이터를 미리 보고 **확인**을 클릭하면 **데이터 미리 보기** 대화 상자가 **원본 테이블 및 뷰 선택** 페이지 또는 **플랫 파일 대상 구성** 페이지로 돌아갑니다. 자세한 내용은 [원본 테이블 및 뷰 선택](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) 또는 [플랫 파일 대상 구성](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)을 참조하세요.  
 
 ## <a name="see-also"></a>참고 항목
[가져오기 및 내보내기 마법사의 이 간단한 예제로 시작](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)
