---
title: "OLE DB 대상 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.oledbdest.f1
- sql13.dts.designer.oledbdestadapter.connection.f1
- sql13.dts.designer.oledbdestadapter.mappings.f1
- sql13.dts.designer.oledbdestadapter.errorhandling.f1
helpviewer_keywords:
- fast-load data access mode [Integration Services]
- OLE DB destination [Integration Services]
- fast load options [Integration Services]
- fast-load options [Integration Services]
- destinations [Integration Services], OLE DB
- fast load data access mode [Integration Services]
- inserting data
ms.assetid: 873a2fa0-2a02-41fc-a80a-ec9767f36a8a
caps.latest.revision: 79
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 7d5bc198ae3082c1b79a3a64637662968b0748b2
ms.openlocfilehash: 4b765081a3897553bef2791bf72631908b5adc2c
ms.contentlocale: ko-kr
ms.lasthandoff: 08/17/2017

---
# <a name="ole-db-destination"></a>OLE DB 대상
  OLE DB 대상은 데이터베이스 테이블이나 뷰 또는 SQL 명령을 사용하여 다양한 OLE DB 호환 데이터베이스로 데이터를 로드합니다. 예를 들어 OLE DB 원본은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 테이블로 데이터를 로드할 수 있습니다.  
  
> [!NOTE]  
>  데이터 원본이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007인 경우 이 데이터 원본에는 이전 버전의 Excel과 다른 연결 관리자가 필요합니다. 자세한 내용은 [Excel 통합 문서에 연결](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)을 참조하세요.  
  
 OLE DB 대상은 데이터 로드를 위한 5가지 데이터 액세스 모드를 제공합니다.  
  
-   테이블 또는 뷰 기존 테이블이나 뷰를 지정하거나 새 테이블을 만들 수 있습니다.  
  
-   빠른 로드 옵션을 사용하는 테이블 또는 뷰. 기존 테이블을 지정하거나 새 테이블을 만들 수 있습니다.  
  
-   변수에 지정된 테이블 또는 뷰  
  
-   빠른 로드 옵션을 사용하는 변수에 지정된 테이블 또는 뷰  
  
-   SQL 문의 결과  
  
> [!NOTE]  
>  OLE DB 대상은 매개 변수를 지원하지 않습니다. 매개 변수가 있는 INSERT 문을 실행해야 하는 경우 OLE DB 명령 변환을 사용하십시오. 자세한 내용은 [OLE DB Command Transformation](../../integration-services/data-flow/transformations/ole-db-command-transformation.md)을 참조하세요.  
  
 OLE DB 대상에서 DBCS(더블바이트 문자 집합)를 사용하는 문자 집합이 로드되는 경우 데이터 액세스 모드에 빠른 로드 옵션이 사용되지 않고 OLE DB 연결 관리자에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQLOLEDB(OLE DB Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] )가 사용되는 경우 데이터가 손상될 수 있습니다. DBCS 데이터의 무결성을 보장하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 사용하도록 OLE DB 연결 관리자를 구성하거나 **테이블 또는 뷰 - 빠른 로드** 또는 **테이블 이름 또는 뷰 이름 변수 - 빠른 로드**와 같은 빠른 로드 액세스 모드 중 하나를 사용해야 합니다. 두 옵션은 모두 **OLE DB 대상 편집기** 대화 상자에서 사용할 수 있습니다. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 개체 모델을 프로그래밍하는 경우 AccessMode 속성을 **FastLoad를 사용한 OpenRowset**또는 **변수와 FastLoad를 사용한 OpenRowset**으로 설정해야 합니다.  
  
> [!NOTE]  
>  OLE DB 대상에서 데이터를 삽입할 대상 테이블을 만들기 위해 **디자이너에서** OLE DB 대상 편집기 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 대화 상자를 사용하는 경우에는 새로 만든 테이블을 수동으로 선택해야 할 수도 있습니다. DB2용 OLE DB 공급자와 같은 OLE DB 공급자에서 테이블 이름에 스키마 식별자를 자동으로 추가하는 경우에는 이렇게 테이블을 수동으로 선택해야 합니다.  
  
> [!NOTE]  
>  **OLE DB 대상 편집기** 대화 상자를 사용하여 생성하는 CREATE TABLE 문은 대상 유형에 따라 수정해야 합니다. 예를 들어 일부 대상은 CREATE TABLE 문에서 사용하는 데이터 형식을 지원하지 않습니다.  
  
 이 대상은 OLE DB 연결 관리자를 사용하여 데이터 원본에 연결하며 연결 관리자가 사용할 OLE DB 공급자를 지정합니다. 자세한 내용은 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)를 참조하세요.  
  
 또한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트는 OLE DB 연결 관리자를 만들 수 있는 데이터 원본 개체를 제공하여 OLE DB 대상에서 데이터 원본과 데이터 원본 뷰를 사용할 수 있게 합니다.  
  
 OLE DB 대상에는 입력 열과 대상 데이터 원본 열 사이의 매핑이 포함됩니다. 입력 열을 모든 대상 열로 매핑할 필요는 없지만 입력 열이 대상 열에 매핑되지 않은 경우 대상 열의 속성에 따라 오류가 발생할 수 있습니다. 예를 들어 대상 열에 Null 값이 허용되지 않는 경우에는 입력 열을 해당 열에 매핑해야 합니다. 또한 매핑된 열의 데이터 형식이 호환되어야 합니다. 예를 들어 문자열 데이터 형식의 입력 열은 숫자 데이터 형식의 대상 열로 매핑할 수 없습니다.  
  
 OLE DB 대상에는 하나의 일반 입력과 하나의 오류 출력이 있습니다.  
  
 데이터 형식에 대한 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
## <a name="fast-load-options"></a>빠른 로드 옵션  
 OLE DB 대상에서 빠른 로드 데이터 액세스 모드를 사용하는 경우 대상에 대해 사용자 인터페이스 **OLE DB 대상 편집기**에서 다음과 같은 빠른 로드 옵션을 지정할 수 있습니다.  
  
-   가져온 데이터 파일에서 ID 값을 유지하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 할당된 고유 값을 사용합니다.  
  
-   대량 로드 작업 중에 발생한 Null 값을 유지합니다.  
  
-   대상 테이블의 제약 조건을 검사하거나 대량 가져오기 작업을 검토합니다.  
  
-   대량 로드 작업이 지속되는 동안 테이블 수준 잠금을 획득합니다.  
  
-   일괄 처리의 행 수 및 커밋 크기를 지정합니다.  
  
 일부 빠른 로드 옵션은 OLE DB 대상의 특정 속성에 저장됩니다. 예를 들어 FastLoadKeepIdentity는 ID 값을 유지할지 여부를 지정하고, FastLoadKeepNulls는 Null 값을 유지할지 여부를 지정하며, FastLoadMaxInsertCommitSize는 일괄 처리로 커밋할 행 수를 지정합니다. 기타 빠른 로드 옵션은 쉼표로 구분된 목록으로 FastLoadOptions 속성에 저장됩니다. OLE DB 대상에서 FastLoadOptions에 저장되고 **OLE DB 대상 편집기** 대화 상자에 나열되는 빠른 로드 옵션을 모두 사용할 경우 속성 값은 **TABLOCK, CHECK_CONSTRAINTS, ROWS_PER_BATCH=1000**으로 설정됩니다. 값 1000은 대상이 1000개의 행을 일괄적으로 사용하도록 구성되었음을 나타냅니다.  
  
> [!NOTE]  
>  대상에서 제약 조건에 맞지 않아 오류가 발생하면 FastLoadMaxInsertCommitSize에 의해 정의된 행에 대한 전체 일괄 처리가 실패하게 됩니다.  
  
 **OLE DB 대상 편집기** 대화 상자에 표시된 빠른 로드 옵션 외에도 **고급 편집기** 대화 상자의 FastLoadOptions 속성에 옵션을 입력하여 다음과 같은 대량 로드 옵션을 사용하도록 OLE DB 대상을 구성할 수 있습니다.  
  
|빠른 로드 옵션|Description|  
|----------------------|-----------------|  
|KILOBYTES_PER_BATCH|삽입할 크기(KB)를 지정합니다. 옵션은 폼 **KILOBYTES_PER_BATCH** = \<양의 정수 값**>**합니다.|  
|FIRE_TRIGGERS|테이블 삽입에 대한 트리거 시작 여부를 지정합니다. 이 옵션은 **FIRE_TRIGGERS**형식으로 입력합니다. 이 옵션이 있으면 트리거가 시작됨을 나타냅니다.|  
|ORDER|입력 데이터 저장 방식을 지정합니다. 옵션은 폼 순서 \<열 이름 > ASC &#124; DESC입니다. 열 수에 상관없이 나열할 수 있으며 정렬 순서를 포함할 수도 있습니다. 정렬 순서를 생략하면 삽입 작업에서는 데이터가 정렬되지 않은 것으로 간주합니다.<br /><br /> 참고: ORDER 옵션을 사용하여 테이블의 클러스터형 인덱스에 따라 입력 데이터를 정렬하면 성능을 개선할 수 있습니다.|  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 키워드는 일반적으로 대문자를 사용하여 입력하지만 키워드는 대/소문자를 구분하지 않습니다.  
  
 빠른 로드 옵션에 대한 자세한 내용은 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)를 참조하세요.  
  
## <a name="troubleshooting-the-ole-db-destination"></a>OLE DB 대상 문제 해결  
 OLE DB 대상이 외부 데이터 공급자에 대해 수행하는 호출을 로깅할 수 있습니다. 이 로깅 기능을 사용하면 OLE DB 대상이 외부 데이터 원본에 데이터를 저장할 때 발생하는 문제를 해결할 수 있습니다. OLE DB 대상이 외부 데이터 공급자에 대해 수행하는 호출을 로깅하려면 패키지 로깅을 설정하고 패키지 수준에서 **Diagnostic** 이벤트를 선택합니다. 자세한 내용은 [패키지 실행 문제 해결 도구](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)를 참조하세요.  
  
## <a name="configuring-the-ole-db-destination"></a>OLE DB 대상 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [공용 속성](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [OLE DB 사용자 지정 속성](../../integration-services/data-flow/ole-db-custom-properties.md)  
  
 속성 설정 방법을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [OLE DB 대상을 사용하여 데이터 로드](../../integration-services/data-flow/load-data-by-using-the-ole-db-destination.md)  
  
-   [데이터 흐름 구성 요소의 속성 설정](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="ole-db-destination-editor-connection-manager-page"></a>OLE DB 대상 편집기(연결 관리자 페이지)
  **OLE DB 대상 편집기** 대화 상자의 **연결 관리자** 페이지를 사용하여 대상에 대한 OLE DB 연결을 선택할 수 있습니다. 이 페이지를 사용하면 데이터베이스에서 테이블이나 뷰를 선택할 수도 있습니다.  
  
> [!NOTE]  
>  데이터 원본이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007인 경우 이 데이터 원본에는 이전 버전의 Excel과 다른 연결 관리자가 필요합니다. 자세한 내용은 [Excel 통합 문서에 연결](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)을 참조하세요.  
  
> [!NOTE]  
>  OLE DB 대상의 **CommandTimeout** 속성은 **OLE DB 대상 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다. 또한 특정 빠른 로드 옵션은 **고급 편집기**에서만 사용할 수 있습니다. 이러한 속성에 대한 자세한 내용은 [OLE DB Custom Properties](../../integration-services/data-flow/ole-db-custom-properties.md)의 OLE DB 대상 섹션을 참조하십시오.  
  
### <a name="static-options"></a>정적 옵션  
 **OLE DB 연결 관리자**  
 목록에서 기존 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 **OLE DB 연결 관리자 구성** 대화 상자를 사용하여 새 연결 관리자를 만듭니다.  
  
 **데이터 액세스 모드**  
 대상으로 데이터를 로드하는 방법을 지정합니다. DBCS(더블바이트 문자 집합) 데이터는 빠른 로드 옵션 중 하나를 사용하여 로드해야 합니다. 대량 삽입에 최적화된 빠른 로드 데이터 액세스 모드에 대한 자세한 내용은 [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md)을 참조하십시오.  
  
|옵션|Description|  
|------------|-----------------|  
|테이블 또는 뷰|OLE DB 대상의 테이블 또는 뷰로 데이터를 로드합니다.|  
|테이블 또는 뷰 - 빠른 로드|빠른 로드 옵션을 사용하여 OLE DB 대상의 테이블 또는 뷰로 데이터를 로드합니다. 대량 삽입에 최적화된 빠른 로드 데이터 액세스 모드에 대한 자세한 내용은 [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md)을 참조하십시오.|  
|테이블 이름 또는 뷰 이름 변수|변수에 테이블 또는 뷰 이름을 지정합니다.<br /><br /> **관련 정보**: [패키지에서 변수 사용](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|테이블 이름 또는 뷰 이름 변수 - 빠른 로드|변수에 테이블 이름 또는 뷰 이름을 지정하고 빠른 로드 옵션을 사용하여 데이터를 로드합니다. 대량 삽입에 최적화된 빠른 로드 데이터 액세스 모드에 대한 자세한 내용은 [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md)을 참조하십시오.|  
|SQL 명령|SQL 쿼리를 사용하여 OLE DB 대상으로 데이터를 로드합니다.|  
  
 **미리 보기**  
 **쿼리 결과 미리 보기** 대화 상자를 사용하여 결과를 미리 봅니다. 미리 보기에는 최대 200개의 행이 표시될 수 있습니다.  
  
### <a name="data-access-mode-dynamic-options"></a>데이터 액세스 모드 동적 옵션  
 각 **데이터 액세스 모드** 설정은 해당 설정에 따라 동적 옵션 집합이 표시됩니다. 다음 섹션에서는 각 **데이터 액세스 모드** 설정에 따라 사용할 수 있는 동적 옵션에 대해 설명합니다.  
  
#### <a name="data-access-mode--table-or-view"></a>데이터 액세스 모드 = 테이블 또는 뷰  
 **테이블 또는 뷰 이름**  
 데이터 원본의 사용 가능한 테이블 또는 뷰 목록에서 테이블 또는 뷰 이름을 선택합니다.  
  
 **새로 만들기**  
 **테이블 만들기** 대화 상자를 사용하여 새 테이블을 만듭니다.  
  
> [!NOTE]  
>  **새로 만들기**를 클릭하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 연결된 데이터 원본에 따라 기본 CREATE TABLE 문을 생성합니다. 원본 테이블에 선언된 FILESTREAM 특성이 포함된 열이 있어도 기본 CREATE TABLE 문은 FILESTREAM 특성을 포함하지 않습니다. FILESTREAM 특성이 포함된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소를 실행하려면 먼저 대상 데이터베이스에서 FILESTREAM 저장소를 구현하십시오. 그런 다음 **테이블 만들기** 대화 상자에서 FILESTREAM 특성을 CREATE TABLE 문에 추가하십시오. 자세한 내용은 [Blob&#40;Binary Large Object&#41; 데이터&#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)를 참조하세요.  
  
#### <a name="data-access-mode--table-or-view--fast-load"></a>데이터 액세스 모드 = 테이블 또는 뷰 - 빠른 로드  
 **테이블 또는 뷰 이름**  
 이 목록을 사용하여 데이터베이스에서 테이블 또는 뷰를 선택하거나 **새로 만들기**를 클릭하여 새 테이블을 만듭니다.  
  
 **새로 만들기**  
 **테이블 만들기** 대화 상자를 사용하여 새 테이블을 만듭니다.  
  
> [!NOTE]  
>  **새로 만들기**를 클릭하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 연결된 데이터 원본에 따라 기본 CREATE TABLE 문을 생성합니다. 원본 테이블에 선언된 FILESTREAM 특성이 포함된 열이 있어도 기본 CREATE TABLE 문은 FILESTREAM 특성을 포함하지 않습니다. FILESTREAM 특성이 포함된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소를 실행하려면 먼저 대상 데이터베이스에서 FILESTREAM 저장소를 구현하십시오. 그런 다음 **테이블 만들기** 대화 상자에서 FILESTREAM 특성을 CREATE TABLE 문에 추가하십시오. 자세한 내용은 [Blob&#40;Binary Large Object&#41; 데이터&#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)를 참조하세요.  
  
 **ID 유지**  
 데이터를 로드할 때 ID 값을 복사할지 여부를 지정합니다. 이 속성은 빠른 로드 옵션을 사용할 때만 사용할 수 있습니다. 이 속성의 기본값은 **false**입니다.  
  
 **Null 유지**  
 데이터를 로드할 때 Null 값을 복사할지 여부를 지정합니다. 이 속성은 빠른 로드 옵션을 사용할 때만 사용할 수 있습니다. 이 속성의 기본값은 **false**입니다.  
  
 **테이블 잠금**  
 로드하는 동안 테이블 잠금을 설정할지 여부를 지정합니다. 이 속성의 기본값은 **true**입니다.  
  
 **CHECK 제약 조건**  
 대상에서 데이터를 로드할 때 제약 조건을 검사할지 여부를 지정합니다. 이 속성의 기본값은 **true**입니다.  
  
 **일괄 처리당 행 수**  
 일괄 처리의 행 수를 지정합니다. 이 속성의 기본값은 값이 할당되지 않음을 나타내는 **-1**입니다.  
  
> [!NOTE]  
>  이 속성에 사용자 지정 값을 할당하지 않으려면 **OLE DB 대상 편집기** 에서 해당 입력란의 내용을 지웁니다.  
  
 **최대 삽입 커밋 크기**  
 OLE DB 대상에서 빠른 로드 작업을 수행하는 동안 커밋을 시도하는 일괄 처리 크기를 지정합니다. 값이 **0** 이면 모든 행이 처리된 다음 모든 데이터가 단일 일괄 처리로 커밋됩니다.  
  
> [!NOTE]  
>  OLE DB 대상 및 다른 데이터 흐름 구성 요소에서 동일한 원본 테이블을 업데이트하는 경우 값 **0** 을 지정하면 실행 중인 패키지가 응답하지 않을 수 있습니다. 패키지가 중지하지 않도록 하려면 **최대 삽입 커밋 크기** 옵션을 **2147483647**로 설정합니다.  
  
 이 속성에 값을 지정하면 대상에서 (1) **최대 삽입 커밋 크기**보다 작은 일괄 처리의 행이나 (2) 현재 처리 중인 버퍼에 남아 있는 행이 커밋됩니다.  
  
> [!NOTE]  
>  대상에서 제약 조건에 맞지 않아 오류가 발생하면 **최대 삽입 커밋 크기** 에 의해 정의된 행에 대한 전체 일괄 처리가 실패하게 됩니다.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>데이터 액세스 모드 = 테이블 이름 또는 뷰 이름 변수  
 **변수 이름**  
 테이블 또는 뷰 이름이 포함된 변수를 선택합니다.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable--fast-load"></a>데이터 액세스 모드 = 테이블 이름 또는 뷰 이름 변수 - 빠른 로드  
 **변수 이름**  
 테이블 또는 뷰 이름이 포함된 변수를 선택합니다.  
  
 **새로 만들기**  
 **테이블 만들기** 대화 상자를 사용하여 새 테이블을 만듭니다.  
  
> [!NOTE]  
>  **새로 만들기**를 클릭하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 연결된 데이터 원본에 따라 기본 CREATE TABLE 문을 생성합니다. 원본 테이블에 선언된 FILESTREAM 특성이 포함된 열이 있어도 기본 CREATE TABLE 문은 FILESTREAM 특성을 포함하지 않습니다. FILESTREAM 특성이 포함된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소를 실행하려면 먼저 대상 데이터베이스에서 FILESTREAM 저장소를 구현하십시오. 그런 다음 **테이블 만들기** 대화 상자에서 FILESTREAM 특성을 CREATE TABLE 문에 추가하십시오. 자세한 내용은 [Blob&#40;Binary Large Object&#41; 데이터&#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)를 참조하세요.  
  
 **ID 유지**  
 데이터를 로드할 때 ID 값을 복사할지 여부를 지정합니다. 이 속성은 빠른 로드 옵션을 사용할 때만 사용할 수 있습니다. 이 속성의 기본값은 **false**입니다.  
  
 **Null 유지**  
 데이터를 로드할 때 Null 값을 복사할지 여부를 지정합니다. 이 속성은 빠른 로드 옵션을 사용할 때만 사용할 수 있습니다. 이 속성의 기본값은 **false**입니다.  
  
 **테이블 잠금**  
 로드하는 동안 테이블 잠금을 설정할지 여부를 지정합니다. 이 속성의 기본값은 **false**입니다.  
  
 **CHECK 제약 조건**  
 태스크에서 제약 조건을 검사할지 여부를 지정합니다. 이 속성의 기본값은 **false**입니다.  
  
 **일괄 처리당 행 수**  
 일괄 처리의 행 수를 지정합니다. 이 속성의 기본값은 값이 할당되지 않음을 나타내는 **-1**입니다.  
  
> [!NOTE]  
>  이 속성에 사용자 지정 값을 할당하지 않으려면 **OLE DB 대상 편집기** 에서 해당 입력란의 내용을 지웁니다.  
  
 **최대 삽입 커밋 크기**  
 OLE DB 대상에서 빠른 로드 작업을 수행하는 동안 커밋을 시도하는 일괄 처리 크기를 지정합니다. 기본값은 **2147483647** 이며 이 경우 모든 행이 처리된 다음 모든 데이터가 단일 일괄 처리로 커밋됩니다.  
  
> [!NOTE]  
>  OLE DB 대상 및 다른 데이터 흐름 구성 요소에서 동일한 원본 테이블을 업데이트하는 경우 값 **0** 을 지정하면 실행 중인 패키지가 응답하지 않을 수 있습니다. 패키지가 중지하지 않도록 하려면 **최대 삽입 커밋 크기** 옵션을 **2147483647**로 설정합니다.  
  
#### <a name="data-access-mode--sql-command"></a>데이터 액세스 모드 = SQL 명령  
 **SQL 명령 텍스트**  
 SQL 쿼리 텍스트를 입력하고 **쿼리 작성**을 클릭하여 쿼리를 작성하거나 **찾아보기**를 클릭하여 쿼리 텍스트가 포함된 파일을 찾습니다.  
  
> [!NOTE]  
>  OLE DB 대상은 매개 변수를 지원하지 않습니다. 매개 변수가 있는 INSERT 문을 실행해야 하는 경우 OLE DB 명령 변환을 사용하십시오. 자세한 내용은 [OLE DB Command Transformation](../../integration-services/data-flow/transformations/ole-db-command-transformation.md)을 참조하세요.  
  
 **Build query**  
 **쿼리 작성기** 대화 상자를 사용하여 시각적으로 SQL 쿼리를 생성할 수 있습니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 SQL 쿼리 텍스트가 포함된 파일을 찾을 수 있습니다.  
  
 **쿼리 구문 분석**  
 쿼리 텍스트의 구문을 확인합니다.  
  
## <a name="ole-db-destination-editor-mappings-page"></a>OLE DB 대상 편집기(매핑 페이지)
  **OLE DB 대상 편집기** 대화 상자의 **매핑** 페이지를 사용하여 입력 열을 대상 열에 매핑할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **사용 가능한 입력 열**  
 사용 가능한 입력 열 목록을 표시합니다. 끌어서 놓기 작업을 사용하여 테이블에서 사용 가능한 입력 열을 대상 열에 매핑합니다.  
  
 **사용 가능한 대상 열**  
 사용 가능한 대상 열의 목록을 표시합니다. 끌어서 놓기 작업을 사용하여 테이블에서 사용 가능한 대상 열을 입력 열에 매핑합니다.  
  
 **입력 열**  
 선택한 입력 열을 표시합니다. 선택 하 여 매핑을 제거할 수 있습니다  **\<무시 >** 출력에서 열을 제외 합니다.  
  
 **대상 열**  
 매핑 여부에 관계없이 사용 가능한 각 대상 열을 표시합니다.  
  
## <a name="ole-db-destination-editor-error-output-page"></a>OLE DB 대상 편집기(오류 출력 페이지)
  **OLE DB 대상 편집기** 대화 상자의 **오류 출력** 페이지를 사용하여 오류 처리 옵션을 지정할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **입/출력**  
 입력 이름을 표시합니다.  
  
 **열**  
 사용되지 않습니다.  
  
 **오류**  
 오류가 발생할 경우 수행할 동작을 지정합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **관련 항목:** [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **잘림**  
 사용되지 않습니다.  
  
 **Description**  
 작업에 대한 설명을 표시합니다.  
  
 **이 값을 선택한 셀에 설정**  
 오류나 잘림 발생 시 선택한 모든 셀에 수행할 동작을 지정합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **적용**  
 선택한 셀에 오류 처리 옵션을 적용합니다.  
  
## <a name="related-content"></a>관련 내용  
 [OLE DB 원본](../../integration-services/data-flow/ole-db-source.md)  
  
 [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md)  
  
 [데이터 흐름](../../integration-services/data-flow/data-flow.md)  
  
  

