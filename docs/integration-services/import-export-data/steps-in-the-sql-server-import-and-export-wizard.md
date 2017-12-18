---
title: "SQL Server 가져오기 및 내보내기 마법사의 단계 | Microsoft Docs"
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 816fb1bd-7bb9-450d-ad65-e4c2d02eaff8
caps.latest.revision: "15"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: aed445a4a884aa07f1fa93a0f27cfe2763bfe4b4
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="steps-in-the-sql-server-import-and-export-wizard"></a>SQL Server 가져오기 및 내보내기 마법사의 단계
이 문서에서는 SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터를 가져오고 내보내는 일련의 단계를 설명합니다. 마법사에 표시되는 각 페이지나 대화 상자를 설명하는 설명서의 개별 페이지에 대한 링크도 포함되어 있습니다.

이 항목에서는 마법사의 **단계**만 설명합니다. 다른 내용을 찾으려면 [관련 태스크 및 콘텐츠](#related)를 참조하세요.

## <a name="steps-for-importing-and-exporting-data"></a>데이터 가져오기 및 내보내기 단계  
 다음 표에서는 데이터 가져오기 및 내보내기 마법사의 단계와 마법사의 해당 페이지를 나열합니다. 마법사에서 선택한 옵션에 따라 일반적으로 일부 페이지가 표시되지 않을 수 있습니다.  

일반적인 세션에서 볼 수 있는 몇 가지 화면을 간략히 보려면 [가져오기 및 내보내기 마법사의 간단한 예제 시작](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md) 단일 페이지에 있는 간단한 종단 간 예제를 살펴봅니다.

|단계|마법사 페이지|  
|----------|------------------|  
|**시작**<br />이 페이지에서는 어떤 작업도 수행할 필요가 없습니다.|[SQL Server 가져오기 및 내보내기 마법사 시작](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)|  
|데이터 **원본을 선택**합니다.|[데이터 원본 선택](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)|  
|데이터의 **대상을 선택**합니다.|[대상 선택](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)|  
|**대상을 구성합니다**. (선택적 단계)<br /><br /> - 새 대상 데이터베이스를 만듭니다.<br />- 텍스트 파일에 데이터를 복사할 경우 추가 설정을 구성합니다.|[데이터베이스 만들기](../../integration-services/import-export-data/create-database-sql-server-import-and-export-wizard.md)<br /><br />[플랫 파일 대상 구성](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)|  
|**복사 대상을 지정합니다.**|[테이블 복사 또는 쿼리 지정](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)<br /><br />[원본 테이블 및 뷰 선택](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)<br /><br />[원본 쿼리 제공](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md)|  
|**복사 작업 구성**합니다. (선택적 단계)<br /><br /> - 새 대상 테이블을 만듭니다.<br />- 마법사에 선택한 원본과 대상 간의 데이터 유형을 매핑하는 방법을 모르는 경우 수행할 작업을 결정합니다.<br />- 원본과 대상 간에 열 매핑을 검토합니다.<br />- 원본과 대상 간의 데이터 형식 변환 문제를 처리합니다.<br />- 복사할 데이터를 미리 봅니다.|[테이블 생성 SQL 문](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)<br /><br />[변환 검사를 수행하지 않고 형식 변환](../../integration-services/import-export-data/convert-types-without-conversion-checking-sql-server-import-and-export-wizard.md)<br /><br />[열 매핑](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)<br /><br />[데이터 형식 매핑 검토](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)<br /><br />[열 변환 정보 대화 상자](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md)<br /><br />[데이터 미리 보기 대화 상자](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)|  
|**데이터를 복사합니다.**<br /><br /> 선택적으로, 설정을 SSIS(SQL Server Integration Services) 패키지로 저장합니다.|[패키지 저장 및 실행](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)<br /><br />[SSIS 패키지 저장](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)<br /><br />[마법사 완료](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)<br /><br />[작업 수행](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md)|  

> [!TIP]
> 마법사의 모든 페이지 또는 대화 상자에서 F1 키를 누르면 현재 페이지에 대한 설명서를 볼 수 있습니다.

## <a name="related"></a> 관련 태스크 및 콘텐츠  
다음은 몇 가지 다른 기본 작업입니다.
-   **마법사의 작동 원리에 대한 빠른 예제를 참조하세요.**

    -   **스크린샷을 보려면.** 단일 페이지([가져오기 및 내보내기 마법사의 간단한 예제 시작](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md))에서 간단한 종단 간 예제를 살펴봅니다.

    -   **비디오를 시청하려면.** 마법사를 보여 주고 Excel로 데이터를 내보내는 방법을 명료하고 간단하게 설명하는 4분 길이의 YouTube 동영상([SQL Server 가져오기 및 내보내기 마법사를 사용하여 Excel로 내보내기](https://go.microsoft.com/fwlink/?linkid=829049))을 시청합니다.

-   **마법사의 작동 원리에 대해 자세히 알아보기.**

    -   **마법사에 대해 자세히 알아보기.** 마법사에 대한 개요를 살펴보려면 [SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터 가져오기 및 내보내기](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)를 참조하세요.

    -   **데이터 원본 및 대상에 연결하는 방법에 대해 자세히 알아보기.** 데이터에 연결하는 방법에 대한 정보를 찾으려면 [SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터 원본에 연결](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md)의 목록에서 원하는 페이지를 선택하세요. 주로 사용되는 각 데이터 원본에 대한 개별 설명서 페이지도 있습니다. 

-   **마법사를 시작합니다.** 마법사 실행 준비를 마치고 시작하는 방법을 알고 싶으면 [SQL Server 가져오기 및 내보내기 마법사 시작](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)을 참조하세요.

-     **마법사를 가져옵니다.** 마법사를 실행하려고 하지만 컴퓨터에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 설치되지 않은 경우 SSDT(SQL Server Data Tools)를 설치하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 설치할 수 있습니다. 자세한 내용은 [SSDT(SQL Server Data Tools) 다운로드](https://msdn.microsoft.com/library/mt204009.aspx)를 참조하세요.


