---
title: OLE DB 대상 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbdest.f1
helpviewer_keywords:
- fast-load data access mode [Integration Services]
- OLE DB destination [Integration Services]
- fast load options [Integration Services]
- fast-load options [Integration Services]
- destinations [Integration Services], OLE DB
- fast load data access mode [Integration Services]
- inserting data
ms.assetid: 873a2fa0-2a02-41fc-a80a-ec9767f36a8a
caps.latest.revision: 77
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: eee342244a6a057a98d5ab6252c6ab970b515118
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37243093"
---
# <a name="ole-db-destination"></a>OLE DB 대상
  OLE DB 대상은 데이터베이스 테이블이나 뷰 또는 SQL 명령을 사용하여 다양한 OLE DB 호환 데이터베이스로 데이터를 로드합니다. 예를 들어 OLE DB 원본은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 테이블로 데이터를 로드할 수 있습니다.  
  
 OLE DB 대상은 데이터 로드를 위한 5가지 데이터 액세스 모드를 제공합니다.  
  
-   테이블 또는 뷰 기존 테이블이나 뷰를 지정하거나 새 테이블을 만들 수 있습니다.  
  
-   빠른 로드 옵션을 사용하는 테이블 또는 뷰. 기존 테이블을 지정하거나 새 테이블을 만들 수 있습니다.  
  
-   변수에 지정된 테이블 또는 뷰  
  
-   빠른 로드 옵션을 사용하는 변수에 지정된 테이블 또는 뷰  
  
-   SQL 문의 결과  
  
> [!NOTE]  
>  OLE DB 대상은 매개 변수를 지원하지 않습니다. 매개 변수가 있는 INSERT 문을 실행해야 하는 경우 OLE DB 명령 변환을 사용하십시오. 자세한 내용은 [OLE DB Command Transformation](transformations/ole-db-command-transformation.md)을 참조하세요.  
  
 OLE DB 대상에서 DBCS(더블바이트 문자 집합)를 사용하는 문자 집합이 로드되는 경우 데이터 액세스 모드에 빠른 로드 옵션이 사용되지 않고 OLE DB 연결 관리자에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQLOLEDB(OLE DB Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] )가 사용되는 경우 데이터가 손상될 수 있습니다. DBCS 데이터의 무결성을 보장하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client를 사용하도록 OLE DB 연결 관리자를 구성하거나 **테이블 또는 뷰 - 빠른 로드** 또는 **테이블 이름 또는 뷰 이름 변수 - 빠른 로드**와 같은 빠른 로드 액세스 모드 중 하나를 사용해야 합니다. 두 옵션은 모두 **OLE DB 대상 편집기** 대화 상자에서 사용할 수 있습니다. 프로그래밍 하는 경우는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 개체 모델 AccessMode 속성을 설정 해야 하면 `OpenRowset Using FastLoad`, 또는 `OpenRowset Using FastLoad From Variable`합니다.  
  
> [!NOTE]  
>  OLE DB 대상에서 데이터를 삽입할 대상 테이블을 만들기 위해 **디자이너에서** OLE DB 대상 편집기 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 대화 상자를 사용하는 경우에는 새로 만든 테이블을 수동으로 선택해야 할 수도 있습니다. DB2용 OLE DB 공급자와 같은 OLE DB 공급자에서 테이블 이름에 스키마 식별자를 자동으로 추가하는 경우에는 이렇게 테이블을 수동으로 선택해야 합니다.  
  
> [!NOTE]  
>  **OLE DB 대상 편집기** 대화 상자를 사용하여 생성하는 CREATE TABLE 문은 대상 유형에 따라 수정해야 합니다. 예를 들어 일부 대상은 CREATE TABLE 문에서 사용하는 데이터 형식을 지원하지 않습니다.  
  
 이 대상은 OLE DB 연결 관리자를 사용하여 데이터 원본에 연결하며 연결 관리자가 사용할 OLE DB 공급자를 지정합니다. 자세한 내용은 [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md)를 참조하세요.  
  
 또한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트는 OLE DB 연결 관리자를 만들 수 있는 데이터 원본 개체를 제공하여 OLE DB 대상에서 데이터 원본과 데이터 원본 뷰를 사용할 수 있게 합니다.  
  
 OLE DB 대상에는 입력 열과 대상 데이터 원본 열 사이의 매핑이 포함됩니다. 입력 열을 모든 대상 열로 매핑할 필요는 없지만 입력 열이 대상 열에 매핑되지 않은 경우 대상 열의 속성에 따라 오류가 발생할 수 있습니다. 예를 들어 대상 열에 Null 값이 허용되지 않는 경우에는 입력 열을 해당 열에 매핑해야 합니다. 또한 매핑된 열의 데이터 형식이 호환되어야 합니다. 예를 들어 문자열 데이터 형식의 입력 열은 숫자 데이터 형식의 대상 열로 매핑할 수 없습니다.  
  
 OLE DB 대상에는 하나의 일반 입력과 하나의 오류 출력이 있습니다.  
  
 데이터 형식에 대한 자세한 내용은 [Integration Services Data Types](integration-services-data-types.md)을 참조하세요.  
  
## <a name="fast-load-options"></a>빠른 로드 옵션  
 OLE DB 대상에서 빠른 로드 데이터 액세스 모드를 사용하는 경우 대상에 대해 사용자 인터페이스 **OLE DB 대상 편집기**에서 다음과 같은 빠른 로드 옵션을 지정할 수 있습니다.  
  
-   가져온 데이터 파일에서 ID 값을 유지하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 할당된 고유 값을 사용합니다.  
  
-   대량 로드 작업 중에 발생한 Null 값을 유지합니다.  
  
-   대상 테이블의 제약 조건을 검사하거나 대량 가져오기 작업을 검토합니다.  
  
-   대량 로드 작업이 지속되는 동안 테이블 수준 잠금을 획득합니다.  
  
-   일괄 처리의 행 수 및 커밋 크기를 지정합니다.  
  
 일부 빠른 로드 옵션은 OLE DB 대상의 특정 속성에 저장됩니다. 예를 들어 FastLoadKeepIdentity는 ID 값을 유지할지 여부를 지정하고, FastLoadKeepNulls는 Null 값을 유지할지 여부를 지정하며, FastLoadMaxInsertCommitSize는 일괄 처리로 커밋할 행 수를 지정합니다. 기타 빠른 로드 옵션은 쉼표로 구분된 목록으로 FastLoadOptions 속성에 저장됩니다. OLE DB 대상 FastLoadOptions에 저장 되 고에 나열 된는 모든 빠른 로드 옵션을 사용 하는 경우는 **OLE DB 대상 편집기** 대화 상자에서 속성의 값 설정할지 `TABLOCK, CHECK_CONSTRAINTS, ROWS_PER_BATCH=1000`합니다. 값 1000은 대상이 1000개의 행을 일괄적으로 사용하도록 구성되었음을 나타냅니다.  
  
> [!NOTE]  
>  대상에서 제약 조건에 맞지 않아 오류가 발생하면 FastLoadMaxInsertCommitSize에 의해 정의된 행에 대한 전체 일괄 처리가 실패하게 됩니다.  
  
 **OLE DB 대상 편집기** 대화 상자에 표시된 빠른 로드 옵션 외에도 **고급 편집기** 대화 상자의 FastLoadOptions 속성에 옵션을 입력하여 다음과 같은 대량 로드 옵션을 사용하도록 OLE DB 대상을 구성할 수 있습니다.  
  
|빠른 로드 옵션|Description|  
|----------------------|-----------------|  
|KILOBYTES_PER_BATCH|삽입할 크기(KB)를 지정합니다. 옵션은 폼 `KILOBYTES_PER_BATCH`  =  \<integer value**>** 합니다.|  
|FIRE_TRIGGERS|테이블 삽입에 대한 트리거 시작 여부를 지정합니다. 이 옵션은 **FIRE_TRIGGERS**형식으로 입력합니다. 이 옵션이 있으면 트리거가 시작됨을 나타냅니다.|  
|ORDER|입력 데이터 저장 방식을 지정합니다. 이 옵션은 ORDER \<열 이름> ASC&#124;DESC 형식으로 입력합니다. 열 수에 상관없이 나열할 수 있으며 정렬 순서를 포함할 수도 있습니다. 정렬 순서를 생략하면 삽입 작업에서는 데이터가 정렬되지 않은 것으로 간주합니다.<br /><br /> 참고: ORDER 옵션을 사용하여 테이블의 클러스터형 인덱스에 따라 입력 데이터를 정렬하면 성능을 개선할 수 있습니다.|  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 키워드는 일반적으로 대문자를 사용하여 입력하지만 키워드는 대/소문자를 구분하지 않습니다.  
  
 빠른 로드 옵션에 대한 자세한 내용은 [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)를 참조하세요.  
  
## <a name="troubleshooting-the-ole-db-destination"></a>OLE DB 대상 문제 해결  
 OLE DB 대상이 외부 데이터 공급자에 대해 수행하는 호출을 로깅할 수 있습니다. 이 로깅 기능을 사용하면 OLE DB 대상이 외부 데이터 원본에 데이터를 저장할 때 발생하는 문제를 해결할 수 있습니다. OLE DB 대상이 외부 데이터 공급자에 대해 수행하는 호출을 로깅하려면 패키지 로깅을 설정하고 패키지 수준에서 **Diagnostic** 이벤트를 선택합니다. 자세한 내용은 [패키지 실행 문제 해결 도구](../troubleshooting/troubleshooting-tools-for-package-execution.md)를 참조하세요.  
  
## <a name="configuring-the-ole-db-destination"></a>OLE DB 대상 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **OLE DB 대상 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [OLE DB 대상 편집기 &#40;연결 관리자 페이지&#41;](../ole-db-destination-editor-connection-manager-page.md)  
  
-   [OLE DB 대상 편집기 &#40;매핑 페이지&#41;](../ole-db-destination-editor-mappings-page.md)  
  
-   [OLE DB 대상 편집기 &#40;오류 출력 페이지&#41;](../ole-db-destination-editor-error-output-page.md)  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](../common-properties.md)  
  
-   [OLE DB 사용자 지정 속성](ole-db-custom-properties.md)  
  
 속성 설정 방법을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [OLE DB 대상을 사용하여 데이터 로드](ole-db-destination.md)  
  
-   [데이터 흐름 구성 요소의 속성 설정](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>관련 내용  
 [OLE DB 원본](ole-db-source.md)  
  
 [Integration Services &#40;SSIS&#41; 변수](../integration-services-ssis-variables.md)  
  
 [데이터 흐름](data-flow.md)  
  
  
