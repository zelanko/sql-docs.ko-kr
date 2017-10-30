---
title: "데이터 대화 상자 (SQL Server 가져오기 및 내보내기 마법사) 미리 보기 | Microsoft Docs"
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.previewdata.f1
ms.assetid: 423ac26a-ba02-4fdf-88b4-07995fe4a97e
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: bfa75d2c1d2d50d1f0205fed22811ddbb3b96747
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="preview-data-dialog-box-sql-server-import-and-export-wizard"></a>데이터 미리 보기 대화 상자(SQL Server 가져오기 및 내보내기 마법사)
  복사할 데이터를 지정한 후 필요에 따라 **미리 보기** 를 클릭하여 **데이터 미리 보기** 대화 상자를 열 수 있습니다. 이 페이지에서는 데이터 원본의 샘플 데이터 행을 최대 200개까지 미리 볼 수 있습니다. 이를 통해 원하는 데이터를 마법사가 복사하는지 확인할 수 있습니다.
  
## <a name="screen-shot-of-the-preview-data-page"></a>데이터 미리 보기 페이지의 스크린샷 
 다음 스크린샷은 마법사의 **데이터 미리 보기** 대화 상자를 보여 줍니다.  
 
![가져오기 및 내보내기 마법사의 미리 보기 데이터 페이지](../../integration-services/import-export-data/media/preview-data.png "가져오기 및 내보내기 마법사의 미리 보기 데이터 페이지")  
  
## <a name="preview-sample-data"></a>샘플 데이터 미리 보기  
 **원본**  
마법사가 데이터 원본에서 데이터를 로드하는 데 사용하는 쿼리를 표시합니다.

복사할 테이블을 선택한 경우에 **소스** 표시 필드는 `SELECT * FROM <table>` 테이블 이름 대신 쿼리 합니다. 
  
 **샘플 데이터 표**  
 쿼리가 데이터 원본에서 반환하는 샘플 데이터의 행을 최대 200개까지 표시합니다.  


## <a name="thats-not-right-i-want-to-change-something"></a>즉 오른쪽을 변경 하려면 하는 경우
데이터를 미리 본 후 마법사의 이전 페이지에서 선택한 옵션을 변경할 수도 있습니다. 이렇게 변경 하려면 클릭 **확인** 돌아가려면는 **원본 테이블 및 뷰 선택** 페이지를 선택한 다음 클릭 **다시** 변경할 수 있는 이전 페이지로 반환 하 여 선택 항목입니다.

## <a name="whats-next"></a>다음 단계  
 복사할 데이터를 미리 보고 **확인**을 클릭하면 **데이터 미리 보기** 대화 상자가 **원본 테이블 및 뷰 선택** 페이지 또는 **플랫 파일 대상 구성** 페이지로 돌아갑니다. 자세한 내용은 [원본 테이블 및 뷰 선택](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) 또는 [플랫 파일 대상 구성](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)을 참조하세요.  
 
 ## <a name="see-also"></a>참고 항목
[가져오기 및 내보내기 마법사의 이 간단한 예제로 시작](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

