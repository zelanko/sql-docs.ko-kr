---
title: OLE DB 원본 | Microsoft Docs
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
- sql12.dts.designer.oledbsource.f1
helpviewer_keywords:
- sources [Integration Services], OLE DB
- OLE DB source [Integration Services]
ms.assetid: f87cc5f6-b078-40f3-9d87-7a65e13e4c86
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b9ff94d28a55da5d199647af200c6179ccadc2d2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37271319"
---
# <a name="ole-db-source"></a>OLE DB 원본
  OLE DB 원본은 데이터베이스 테이블, 뷰 또는 SQL 명령을 사용하여 다양한 OLE DB 호환 관계형 데이터베이스에서 데이터를 추출합니다. 예를 들어 OLE DB 원본은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 테이블에서 데이터를 추출할 수 있습니다.  
  
 OLE DB 원본은 데이터 추출을 위한 4가지 데이터 액세스 모델을 제공합니다.  
  
-   테이블 또는 뷰  
  
-   변수에 지정된 테이블 또는 뷰  
  
-   SQL 문의 결과 쿼리는 매개 변수가 있는 쿼리일 수 있습니다.  
  
-   변수에 저장된 SQL 문의 결과  
  
> [!NOTE]  
>  SQL 문을 사용하여 임시 테이블의 결과를 반환하는 저장 프로시저를 호출하는 경우 WITH RESULT SETS 옵션을 사용하여 결과 집합의 메타데이터를 정의합니다.  
  
 매개 변수가 있는 쿼리를 사용하는 경우 변수를 매개 변수에 매핑하여 SQL 문의 개별 매개 변수에 값을 지정할 수 있습니다.  
  
 이 원본은 OLE DB 연결 관리자를 사용하여 데이터 원본에 연결하며 이 연결 관리자는 사용할 OLE DB Provider를 지정합니다. 자세한 내용은 [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md)를 참조하세요.  
  
 또한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트는 OLE DB 연결 관리자를 만들 수 있는 데이터 원본 개체를 제공하여 OLE DB 원본에서 데이터 원본과 데이터 원본 뷰를 사용할 수 있게 합니다.  
  
 OLE DB Provider에 따라 OLE DB 원본에는 다음 몇 가지 제한이 적용됩니다.  
  
-   Oracle용 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider는 Oracle 데이터 형식 BLOB, CLOB, NCLOB, BFILE 또는 UROWID를 지원하지 않으며 OLE DB 원본은 이러한 데이터 형식의 열이 포함된 테이블에서 데이터를 추출할 수 없습니다.  
  
-   IBM OLE DB DB2 공급자와 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB DB2 공급자는 저장 프로시저를 호출하는 SQL 명령의 사용을 지원하지 않습니다. 이러한 종류의 명령을 사용하면 OLE DB 원본에서 열 메타데이터를 만들 수 없으므로 데이터 흐름에서 OLE DB 원본을 따르는 데이터 흐름 구성 요소가 열 데이터를 사용할 수 없으며 데이터 흐름의 실행이 실패합니다.  
  
 OLE DB 원본에는 하나의 일반 출력 및 하나의 오류 출력이 있습니다.  
  
## <a name="using-parameterized-sql-statements"></a>매개 변수가 있는 SQL 문 사용  
 OLE DB 원본은 SQL 문을 사용하여 데이터를 추출할 수 있습니다. 이 문은 SELECT 또는 EXEC 문일 수 있습니다.  
  
 OLE DB 원본은 OLE DB 연결 관리자를 사용하여 데이터를 추출할 데이터 원본에 연결합니다. OLE DB 연결 관리자가 사용하는 공급자 및 연결하는 RDBMS(관계형 데이터베이스 관리 시스템)에 따라 매개 변수 명명 및 나열 작업에 적용되는 규칙이 달라집니다. RDBMS에서 매개 변수 이름을 반환하는 경우 매개 변수 이름을 사용하여 매개 변수 목록의 매개 변수를 SQL 문의 매개 변수에 매핑할 수 있습니다. 그렇지 않으면 매개 변수가 매개 변수 목록에서의 서수 위치별로 SQL 문의 매개 변수에 매핑됩니다. 지원되는 매개 변수 이름 유형은 공급자에 따라 달라집니다. 예를 들어 일부 공급자의 경우 변수 또는 열 이름을 사용해야 하지만 0 또는 Param0과 같은 심볼 이름을 사용해야 하는 공급자도 있습니다. SQL 문에서 사용할 매개 변수 이름에 대한 자세한 내용은 공급자별 설명서를 참조하십시오.  
  
 OLE DB 연결 관리자를 사용하는 경우에는 OLE DB 원본이 OLE DB Provider를 통해 매개 변수 정보를 파생할 수 없으므로 매개 변수가 있는 하위 쿼리를 사용할 수 없습니다. 하지만 식을 사용하여 매개 변수 값을 쿼리 문자열에 연결하고 원본의 SqlCommand 속성을 설정할 수 있습니다. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 **OLE DB 원본 편집기** 대화 상자를 사용하여 OLE DB 원본을 구성하고 **쿼리 매개 변수 설정** 대화 상자에서 매개 변수를 변수에 매핑합니다.  
  
### <a name="specifying-parameters-by-using-ordinal-positions"></a>서수 위치를 사용하여 매개 변수 지정  
 매개 변수 이름이 반환되지 않는 경우 매개 변수가 **쿼리 매개 변수 설정** 대화 상자의 **매개 변수** 목록에 나열되는 순서에 따라 런타임에 매핑되는 대상 매개 변수 표식이 결정됩니다. 목록의 첫 번째 매개 변수는 SQL 문의 첫 번째 ?에 매핑되고 두 번째 매개 변수는 두 번째 ?에 매핑되는 식입니다.  
  
 다음 SQL 문은 **데이터베이스의** Product [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 테이블에서 행을 선택합니다. **매핑** 목록의 첫 번째 매개 변수는 **Color** 열의 첫 번째 매개 변수에 매핑되고 두 번째 매개 변수는 **Size** 열에 매핑됩니다.  
  
 `SELECT * FROM Production.Product WHERE Color = ? AND Size = ?`  
  
 매개 변수 이름은 영향을 받지 않습니다. 예를 들어 매개 변수의 이름이 적용될 열의 이름과 같지만 해당 매개 변수가 **매개 변수** 목록의 올바른 서수 위치에 배치되어 있지 않은 경우 런타임에 매개 변수 매핑이 수행될 때는 매개 변수의 이름이 아니라 매개 변수의 서수 위치가 사용됩니다.  
  
 EXEC 명령을 사용하려면 일반적으로 프로시저의 매개 변수 값을 매개 변수 이름으로 제공하는 변수의 이름을 사용해야 합니다.  
  
### <a name="specifying-parameters-by-using-names"></a>이름을 사용하여 매개 변수 지정  
 RDBMS에서 실제 매개 변수 이름을 반환하는 경우 SELECT 및 EXEC 문에서 사용하는 매개 변수가 이름별로 매핑됩니다. 매개 변수 이름은 SELECT 문이나 EXEC 문으로 실행되는 저장 프로시저에 필요한 이름과 일치해야 합니다.  
  
 다음 SQL 문은 **데이터베이스에서 사용할 수 있는** uspGetWhereUsedProductID [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 저장 프로시저를 실행합니다.  
  
 `EXEC uspGetWhereUsedProductID ?, ?`  
  
 이 저장 프로시저에는 매개 변수 값을 제공할 변수 `@StartProductID` 및 `@CheckDate`가 필요합니다. **매핑** 목록에 매개 변수가 나타나는 순서는 상관없으며 @을 포함한 매개 변수 이름이 저장 프로시저의 변수 이름과 일치하기만 하면 됩니다.  
  
### <a name="mapping-parameters-to-variables"></a>변수에 매개 변수 매핑  
 매개 변수는 런타임에 매개 변수 값을 제공하는 변수에 매핑됩니다. 변수는 일반적으로 사용자 정의 변수이지만 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 제공하는 시스템 변수를 사용할 수도 있습니다. 사용자 정의 변수를 사용하는 경우에는 매핑된 매개 변수가 참조하는 열의 데이터 형식과 호환되는 형식으로 데이터 형식을 설정합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../integration-services-ssis-variables.md)를 참조하세요.  
  
## <a name="troubleshooting-the-ole-db-source"></a>OLE DB 원본 문제 해결  
 OLE DB 원본이 외부 데이터 공급자에 대해 수행하는 호출을 로깅할 수 있습니다. 이 로깅 기능을 사용하면 OLE DB 원본이 외부 데이터 원본에서 데이터를 로드할 때 발생하는 문제를 해결할 수 있습니다. OLE DB 원본이 외부 데이터 공급자에 대해 수행하는 호출을 로깅하려면 패키지 로깅을 설정하고 패키지 수준에서 **Diagnostic** 이벤트를 선택합니다. 자세한 내용은 [패키지 실행 문제 해결 도구](../troubleshooting/troubleshooting-tools-for-package-execution.md)를 참조하세요.  
  
## <a name="configuring-the-ole-db-source"></a>OLE DB 원본 구성  
 프로그래밍 방식을 통해 또는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하여 속성을 설정할 수 있습니다.  
  
 **OLE DB 원본 편집기** 대화 상자에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [OLE DB 원본 편집기 &#40;연결 관리자 페이지&#41;](../ole-db-source-editor-connection-manager-page.md)  
  
-   [OLE DB 원본 편집기 &#40;열 페이지&#41;](../ole-db-source-editor-columns-page.md)  
  
-   [OLE DB 원본 편집기 &#40;오류 출력 페이지&#41;](../ole-db-source-editor-error-output-page.md)  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](../common-properties.md)  
  
-   [OLE DB 사용자 지정 속성](ole-db-custom-properties.md)  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [OLE DB 원본을 사용하여 데이터 추출](ole-db-source.md)  
  
-   [쿼리 매개 변수를 데이터 흐름 구성 요소의 변수에 매핑](map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [데이터 흐름 구성 요소의 속성 설정](set-the-properties-of-a-data-flow-component.md)  
  
-   [병합 및 병합 조인 변환을 위한 데이터 정렬](transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-content"></a>관련 내용  
 social.technet.microsoft.com의 Wiki 문서 - [Oracle 커넥터가 있는 SSIS](http://go.microsoft.com/fwlink/?LinkId=220670)  
  
## <a name="see-also"></a>관련 항목  
 [OLE DB 대상](ole-db-destination.md)   
 [Integration Services &#40;SSIS&#41; 변수](../integration-services-ssis-variables.md)   
 [데이터 흐름](data-flow.md)  
  
  
