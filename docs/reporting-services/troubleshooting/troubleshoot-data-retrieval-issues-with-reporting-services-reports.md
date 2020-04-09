---
title: Reporting Services 보고서에서 데이터 검색 문제 해결
description: 이 문서에서는 보고서를 로컬로 미리 보거나 보고서 서버에서 보고서를 실행하여 보고서 데이터를 검색할 때 발생하는 문제를 진단하고 해결합니다.
ms.date: 02/27/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: 7680946a-1660-4b59-a03a-c4d474cd8ed3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d62cff71d6967203ab3980624b1f7b192fb89906
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664456"
---
# <a name="troubleshoot-data-retrieval-issues-with-reporting-services-reports"></a>Reporting Services 보고서에서 데이터 검색 문제 해결
보고서 처리의 첫 번째 단계는 데이터 세트 쿼리를 실행하여 각 데이터 세트에 대한 보고서 데이터를 검색하는 것입니다. 보고서를 로컬로 미리 볼 때 데이터 원본 연결 및 자격 증명은 충분한 권한을 사용하여 데이터를 컴퓨터로 읽어 들여야 합니다. 보고서 서버에서 보고서를 실행할 때 데이터 원본 연결 및 자격 증명은 충분한 권한을 사용하여 보고서 서버에서 데이터를 검색해야 합니다. 이 항목을 사용하여 보고서 데이터 검색 관련 문제를 해결할 수 있습니다.   
  
## <a name="i-cannot-create-a-connection-to-a-data-source"></a>데이터 원본에 대한 연결을 만들 수 없는 경우  
데이터 원본을 만들거나, 데이터 세트 쿼리를 실행하거나, 보고서를 미리 볼 때 '데이터 원본 `<data source name>`에 대한 연결을 설정할 수 없습니다.'라는 메시지가 표시될 수 있습니다.   
    
### <a name="data-source-is-not-available"></a>데이터 원본을 사용할 수 없는 경우  
데이터 원본은 여러 이유로 인해 오프라인 상태가 되거나 사용할 수 없게 될 수 있습니다.   
  
데이터 원본에 대한 액세스 권한이 있고 데이터 원본을 사용할 수 있는지 확인합니다. 예를 들어 SQL Server Management Studio를 사용하여 데이터 원본에 연결합니다. 관계형 데이터베이스 및 다차원 데이터베이스의 경우 **연결 속성** 대화 상자의 **테스트** 단추를 사용하여 데이터 원본에 대한 연결 및 권한을 확인할 수 있습니다.   
  
### <a name="data-source-credentials-are-not-valid"></a>데이터 원본 자격 증명이 유효하지 않은 경우  
데이터 원본에 연결하기 위해 사용 중인 자격 증명에 쿼리에 지정된 데이터를 검색하는 데 필요한 권한이 충분하지 않습니다.  
  
사용 중인 자격 증명이 올바른지 확인합니다. 예를 들어 테이블 또는 뷰에서 데이터를 검색할 수는 있지만 특정 열에 대한 사용 권한이 없거나 뷰를 채우는 저장 프로시저를 실행하는 데 충분한 권한이 없을 수도 있습니다.   
  
> [!NOTE]  
> 보고서를 미리 보기 위해 데이터를 검색하는 데 사용하는 권한은 보고서를 보고서 서버에 게시한 후 데이터를 검색하는 데 필요한 권한과 다를 수 있습니다.   
  
### <a name="not-a-valid-password"></a>암호가 유효하지 않은 경우  
입력 정보를 요청하는 자격 증명 또는 연결 문자열에 지정된 자격 증명을 사용하는 데이터 원본의 경우 암호에 입력한 문자는 기본 데이터 원본 드라이버로 전달됩니다. 암호 또는 문자열에 문장 부호와 같은 특수 문자가 포함된 경우 일부 데이터 원본 드라이버는 이러한 특수 문자의 유효성을 검사할 수 없습니다.   
  
암호에 특수 문자가 포함되어 있지 않은지 확인합니다. 암호 변경이 불가능한 경우 데이터베이스 관리자에게 문의하여 해당 자격 증명을 로컬에 저장하고 서버에 시스템 ODBC DSN(데이터 원본 이름)의 일부로 저장합니다. 자세한 내용은 MSDN에 있는 .NET Framework SDK 설명서의 "OdbcConnection.ConnectionString"을 참조하세요.   
  
> [!NOTE]  
>연결 문자열에 암호와 같은 로그인 정보를 추가하지 않는 것이 좋습니다. 보고서 디자이너에서는 자격 증명을 입력하는 데 사용할 수 있는 **데이터 원본 속성** 또는 **공유 데이터 원본 속성** 대화 상자에 **자격 증명** 페이지를 제공합니다. 이러한 자격 증명은 보고서 제작 컴퓨터에 안전하게 저장됩니다.  
  
## <a name="why-do-i-see-no-data-when-i-run-my-query-in-the-query-designer"></a>쿼리 디자이너에서 쿼리를 실행할 때 데이터가 표시되지 않는 이유  
데이터 세트를 만들 때 데이터 세트 필드 컬렉션이 보고서 데이터 창에 표시됩니다. 일부 경우에는 데이터 세트 필드 컬렉션이 예상대로 표시되지 않습니다.   
  
### <a name="import-query-does-not-import-calculated-fields"></a>쿼리를 가져올 때 계산 필드를 가져올 수 없는 경우  
  
보고서 정의에 계산 필드가 저장되어 있어도 다른 보고서에서 데이터 세트 쿼리를 가져올 때 이러한 계산 필드는 포함되지 않습니다. 다른 보고서에서 쿼리를 가져와서 데이터 세트를 만들면 데이터 세트 쿼리로 지정된 필드만 보고서 데이터 창에 표시됩니다.   
  
보고서 데이터 창에서 계산 필드를 보려면 해당 필드가 사용되는 각 보고서에 대해 계산 필드를 정의해야 합니다.   
  
### <a name="some-data-providers-do-not-support-automatic-population-of-the-dataset-field-collection"></a>일부 데이터 공급자가 데이터 세트 필드 컬렉션의 자동 채우기를 지원하지 않는 경우  
데이터 세트 속성 대화 상자에서 쿼리를 정의하고 대화 상자를 닫으면 데이터 세트 필드 컬렉션이 일반적으로 보고서 데이터 창에 표시됩니다. 일부 데이터 원본의 경우 데이터 세트 필드 컬렉션이 자동으로 채워지지 않습니다.   
  
데이터 세트 필드 컬렉션을 채우려면 다음을 수행합니다.  
* 데이터베이스에서 필드 정보를 검색할 수 있는 권한이 있는지 확인합니다. 일부 데이터 원본의 경우 데이터 원본에 액세스할 수는 있지만 테이블이나 열에 대한 사용 권한은 없을 수 있습니다. 뷰에 액세스할 수는 있지만 뷰를 만드는 저장 프로시저를 실행할 수 있는 사용 권한은 없을 수 있습니다. 데이터베이스의 특정 테이블 또는 열에 대한 액세스 권한이 유효한지 검사하려면 보고서에 사용하는 것과 동일한 권한을 사용하여 SQL Server Management Studio와 같은 별도의 애플리케이션에서 쿼리 결과를 확인합니다. 쿼리에 대해 원하는 결과를 볼 수 없는 경우 시스템 관리자에게 문의하여 데이터에 대한 사용 권한을 조정합니다.   
* **데이터 세트 속성** 대화 상자의 쿼리 창에서 쿼리를 실행합니다. 자세한 내용은 [보고서 데이터 세트(보고서 작성기 3.0 및 SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)를 참조하세요.  
* 수동으로 필드를 추가합니다. 자세한 내용은 [방법: 보고서 데이터 창에서 필드 추가, 편집, 새로 고침(보고서 작성기 3.0 및 SSRS)](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)을 참조하세요.   
  
## <a name="see-also"></a>참고 항목  
[오류 및 이벤트(Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]



