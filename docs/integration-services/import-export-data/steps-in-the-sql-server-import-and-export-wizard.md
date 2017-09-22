---
title: "SQL Server 가져오기 및 내보내기 마법사의 단계를 | Microsoft Docs"
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 816fb1bd-7bb9-450d-ad65-e4c2d02eaff8
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: dcd4329c30108f85174e65bb5e9f9dc9d7296bd0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/21/2017

---
# <a name="steps-in-the-sql-server-import-and-export-wizard"></a>SQL Server 가져오기 및 내보내기 마법사의 단계
이 항목에서는 일련의 SQL Server 가져오기 및 내보내기 마법사와 데이터 가져오기 및 내보내기에 대 한 단계를 설명 합니다. 또한 각 페이지에 설명 하는 설명서 또는 대화 상자는 마법사에 표시의 개별 페이지에 대 한 링크를 포함 합니다.

이 항목에서는 설명는 **단계** 마법사에서. 다른 작업에 대 한 찾고 있는 경우 참조 [관련 콘텐츠 및 작업](#related)합니다.

## <a name="steps-for-importing-and-exporting-data"></a>데이터 가져오기 및 내보내기 단계  
 다음 표에서는 데이터 가져오기 및 내보내기 마법사의 단계와 마법사의 해당 페이지를 나열합니다. 마법사에서 선택한 옵션에 따라 일반적으로 이러한 모든 페이지 표시 되지 않는 합니다.  

일반적인 세션에서 여러 화면을 빠르게 확인에 대 한 살펴보세요이 간단한 종단 간 예제를 한 페이지- [가져오기 및 내보내기 마법사의이 간단한 예제 시작](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)합니다.

|단계|마법사 페이지|  
|----------|------------------|  
|**시작**<br />이 페이지에서는 어떤 작업도 수행할 필요가 없습니다.|[SQL Server 가져오기 및 내보내기 마법사 시작](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)|  
|데이터 **원본을 선택**합니다.|[데이터 원본 선택](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)|  
|데이터의 **대상을 선택**합니다.|[대상 선택](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)|  
|**대상 구성**합니다. (선택적 단계)<br /><br /> - 새 대상 데이터베이스를 만듭니다.<br />- 텍스트 파일에 데이터를 복사할 경우 추가 설정을 구성합니다.|[데이터베이스 만들기](../../integration-services/import-export-data/create-database-sql-server-import-and-export-wizard.md)<br /><br />[플랫 파일 대상 구성](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)|  
|**복사를 지정 합니다.**|[테이블 복사 또는 쿼리 지정](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)<br /><br />[원본 테이블 및 뷰 선택](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)<br /><br />[원본 쿼리 지정](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md)|  
|**복사 작업을 구성**합니다. (선택적 단계)<br /><br /> - 새 대상 테이블을 만듭니다.<br />-수행할 작업을 결정 하는 경우 마법사는 원본 및 선택한 대상 간에 데이터 형식을 매핑하는 방법을 모릅니다.<br />- 원본과 대상 간에 열 매핑을 검토합니다.<br />- 원본과 대상 간의 데이터 형식 변환 문제를 처리합니다.<br />- 복사할 데이터를 미리 봅니다.|[테이블 생성 SQL 문](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)<br /><br />[변환 검사 하지 않고 형식 변환](../../integration-services/import-export-data/convert-types-without-conversion-checking-sql-server-import-and-export-wizard.md)<br /><br />[열 매핑](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)<br /><br />[데이터 형식 매핑 검토](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)<br /><br />[열 변환 정보 대화 상자](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md)<br /><br />[데이터 미리 보기 대화 상자](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)|  
|**데이터를 복사 합니다.**<br /><br /> 필요에 따라 설정을 SQL Server Integration Services (SSIS) 패키지도 저장 합니다.|[저장 하 고 패키지를 실행 합니다.](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)<br /><br />[SSIS 패키지 저장](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)<br /><br />[마법사 완료](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)<br /><br />[작업을 수행합니다.](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md)|  

> [!TIP]
> 마법사의 모든 페이지 또는 대화 상자에서 F1 키를 누르면 현재 페이지에 대한 설명서를 볼 수 있습니다.

## <a name="related"></a>관련된 태스크 및 콘텐츠  
다음은 몇 가지 다른 기본 작업입니다.
-   **마법사의 작동 원리에 대 한 빠른 예제를 참조 하십시오.**

    -   **스크린 샷을 참조 하려는 경우** 이 간단한 종단 간 예제를 살펴보세요 단일 페이지- [가져오기 및 내보내기 마법사의이 간단한 예제 시작](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)합니다.

    -   **비디오를 시청 하려면.** YouTube 마법사를 보여 줍니다. 하 고 명확 하 게 설명 하 고 간단 하 게-Excel로 데이터를 내보내는 방법에서이 분 비디오를 시청 [SQL Server 가져오기 및 내보내기 마법사를 Excel로 내보낼 수를 사용 하 여](https://go.microsoft.com/fwlink/?linkid=829049)합니다.

-   **마법사의 작동 방식에 대해 자세히 알아보기**

    -   **마법사에 대해 자세히 알아보기** 마법사에 대한 개요를 살펴보려면 [SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터 가져오기 및 내보내기](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)를 참조하세요.

    -   **데이터 원본 및 대상에 연결 하는 방법을 알아봅니다.** 데이터에 연결 하는 방법에 대 한 정보를 찾고 있는 경우 여기-목록에서 원하는 페이지를 선택 [SQL Server 가져오기 및 내보내기 마법사와 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md)합니다. 각 몇 가지 자주 사용 되는 데이터 원본에 대 한 설명서의 개별 페이지가 있습니다. 

-   **마법사를 시작 합니다.** 마법사 실행 준비를 마치고 시작하는 방법을 알고 싶으면 [SQL Server 가져오기 및 내보내기 마법사 시작](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)을 참조하세요.

-   **마법사를 가져옵니다.** 마법사를 실행 하려고 하지만 없는 경우 [! 포함[msCoName](/sql-docs/docs/ssdt/download-sql-server-data-tools-ssdt)합니다.



